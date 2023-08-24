---
title: opencv stereo rectify 사용법
tags: cv
---

stereo vision에서 depth를 이용할때, rectify를 이용하면 계산이 조금 더 간단해 집니다.(사실 여전히 간단한진 잘 모르겠습니다) 저는 두 카메라에서의 특징점 discriptor를 더 수월하게 찾기 위해서 사용했습니다. 
다만 인터넷상에 opencv stereo rectify 함수를 이용해 world coordinates 의 좌표를 구하는 포스팅은 별로 없어 보입니다.

일단 카메라 파라메터와 에피폴라에 대한 이해가 필요합니다.
이 문서에서 설명하는 전체적인 과정은 다음과 같습니다.
opencv의 stereoRectify 함수를 이용해서 두 카메라에서 rectified 이미지를 얻어냅니다.
여러 방법으로 특징점을 찾아 두 이미지간 특징점을 매치 합니다. 그 점의 카메라별 rectified 이미지 상 x,y 좌표는 즉 **rectified image coordinates** 의 좌표입니다. 그 점을 opencv의 triangulatePoints 함수로 **rectified camera coordinates** 로 변환합니다. 해당 점을 **unrectifyed camera coordinates**로 변환한뒤 extrinsic matrix를 이용해서 **world coordinates** 로 변환 합니다.
  
## stereoRectify 함수
[opencv의 stereoRectify](https://docs.opencv.org/4.x/d9/d0c/group__calib3d.html#ga617b1685d4059c6040827800e72ad2b6) 함수를 보면, 인풋과 아웃풋은 다음과 같습니다.
- input
  - cameraMatrixN: N번 카메라의 intrinsic matrix 입니다.
  - distCoeffsN: N번 카메라의 렌즈 디스토션에 대한 파라메터입니다.
  - imageSize: 입력되는 이미지의 사이즈 입니다.
  - R: 첫번째 카메라에서 두번째 카메라로의 Rotation matrix 입니다.
  - T: 첫번째 카메라에서 두번째 카메라로의 Translation vector 입니다.
- output
  - R*: N번째 카메라에서 rectification transform 을 수행하는 rotation matrix 입니다. 
  - P*: N번째 카메라에서 rectified coordinate projection matrix 입니다. 
  - Q: 4x4 disparity-to-depth mapping matrix
    
input인 R,T의 경우, stereoCalibrate 함수를 이용해 카메라를 캘리브레이션 하면 구해지는 값입니다.
그런데 카메라를 따로따로 캘리브레이션 했다면 다음과 같이 구할 수도 있습니다.
카메라1, 카메라2의 rotation matrix $R_1, R_2$, Translation vector $T_1, T_2$가 있을때 카메라1 에서 카메라2로 rotation matrix $R$과 translation vector $T$는 다음과 같은 식이 성립됩니다.

$$\begin{matrix}
    R_2&=&RR_1 \\
    T_2&=&RT_1 + T
\end{matrix}$$
즉 inverse matrix를 곱하면 $R$과 $T$를 구할 수 있습니다.

$$\begin{matrix}
    R&=&R_2R_1^{-1}\\
    T &=& T_2-RT_1
\end{matrix}$$

output의 R, P 는 다음과 같습니다.
R1,R2는 rotation matrix로, rectify 하기전(unrectified)의 **camera coordinates** (unrectified camera coordinates라고 하겠습니다) 에서의 좌표를 rectify 후의 **camera coordinates** (rectified camera coordinates 라고 하겠습니다.) 로 변환합니다.
  
P1, P2는 rectified camera coordinate에서 rectified image coordinate로 변환하는 projection matrix 입니다. 
이전에 보았던 카메라 파라메터를 기억하시나요? 아래 식에서 $A[R \mid t]$ 와 동일합니다. 
$$s\begin{bmatrix}
        x\\y\\1
    \end{bmatrix}
    = A[R \mid t]
    \begin{bmatrix}
        X\\Y\\Z\\1
    \end{bmatrix}$$
## rectified image 좌표를 reconstruction 하기
그러면 우리가 최종적으로 하고자 하는 목표, 3d reconstruction을 위해서는 다음과 같은 과정이 필요합니다.
구한 좌표는 rectified image coordinates 상의 좌표입니다. 이를 $P_{ri}$ 라고 합시다.
[opencv triangulatePoints](https://docs.opencv.org/4.x/d9/d0c/group__calib3d.html#gad3fc9a0c82b08df034234979960b778c) 문서를 보면, **If the projection matrices from stereoRectify are used, then the returned points are represented in the first camera's rectified coordinate system.** 라고 되어있습니다. 즉 triangulate를 수행하면, 첫번째 카메라의 **rectified camera coordinate** 에서의 3d 점이 반환 됩니다. 이 점을 $P_{rc}$ 라고 합시다. 그러면 **unrectified camera coordinate** 의 점 $P_c$ 와는 다음과 같은 식이 성립합니다.
$$P_{rc} = R_1P_c \\ P_c = R_1^{-1}P_{rc}$$
이점을 world coordinate로 변환하기 위해선, 다시 카메라 파라메터 식을 생각해 보면 됩니다. 간단하게 world coordinate의 점을 $P_w$ 이미지상의 좌표를 $P_i$ 라고 합시다. 
$$P_i = A[R \mid t]P_w$$
이 식의 정의는, $[R \mid t]$가 점을 world coordinates 에서 camera coordinates로 변환하고, A 가 camera coordinates에서 이미지 평면으로 변환하는 식이였습니다. 즉, 
$$P_c = [R \mid t]P_w$$ 
이므로 우리는 extrinsic matrix를 inverse 해서 곱하면 camera coordinates에서 world coordinates로 변환 할수있습니다.

이 과정을 코드로 구현하면 다음과 같습니다.
```python
rectified_cam0_image_points = ... # image coordinates point from rectified image
rectified_cam1_image_points = ... # image coordinates point from rectified image
extrinsic_matrix_0 = ... # camera 1 extrinsic matrix (4x4)
R1, P1, P2 = ... # output of cv2.stereoRectify

rectified_camera_coordinates = cv2.triangulatePoints(
            P1,
            P2,
            rectified_cam0_image_points,
            rectified_cam1_image_points,
        )
rectified_camera_coordinates = triangulated_points[:3, :] / triangulated_points[3, :]

R1_inv = np.linalg.inv(R1)
# rectified camera coordinates to unrectified camera coordinates
unrectified_camera_coordinates = np.dot(
    R1_inv, rectified_camera_coordinates
).T

extrinsic_matrix_0_inv = np.linalg.inv(extrinsic_matrix_0)
# point to homogeneous
unrectified_camera_coordinates = cv2.convertPointsToHomogeneous(
    unrectified_camera_coordinates
)
unrectified_camera_coordinates = unrectified_camera_coordinates.reshape(-1, 4).T
# unrectified camera coordinates to world coordinates
world_coordinates = np.dot(extrinsic_matrix_0_inv, unrectified_camera_coordinates)
```