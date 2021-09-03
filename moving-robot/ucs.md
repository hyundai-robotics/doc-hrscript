# 5.5 사용자좌표계 \(UCS ; User Coordinate System\)

사용자좌표계는 사용자가 위치와 방향을 설정할 수 있는 좌표계입니다.

사용자좌표계는 생성자 함수 Ucs\( \)를 호출하여 생성합니다. 



함수 매개변수는 포즈 1개 혹은 포즈 3개입니다. 포즈 1개로 호출하면, 포즈의 위치와 방향이 좌표계의 원점과 방향으로 설정됩니다. 포즈 3개로 호출하면 pose1의 위치가 좌표계 원점, pose2의 위치가 좌표계 X축, pose3 위치가 좌표계 XY평면 상에 있도록 좌표계가 생성됩니다.

```python
var UCS변수명 = Ucs(pose1)
var UCS변수명 = Ucs(pose1, pose2, pose3)
```

시스템에 사용자좌표계를 등록하려면 mkucs 함수를 사용합니다. 인수는 Ucs 생성자와 비슷하지만 첫 번째 인수로서 사용자좌표계 번호\(1 이상\)가 입력됩니다.

```python
var res = mkucs(num, pose1)
var res = mkucs(num, pose1, pose2, pose3)
```

성공하면 0, 실패하면 에러코드를 음수로 리턴합니다.

