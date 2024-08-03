## 게임 개발 요약
### 07-31
+ #### 프로젝트 Git연동함.
+ #### 플레이어 캐릭터 이동 및 달리기 구현함.
  
### 08-01
+ #### 플레이어 점프 구현함.
+ #### 착지하자마자 바로 점프할수 없도록 타이머를 이용하여 점프를 개선함.
+ #### AnimNotify에서 해당 타이머를 작동 시키는 함수를 호출하여, 착지 애니메이션이 나오고 일정 시간이 지나면 점프 할수 있도록 개선 함.

### 08-02
+ #### BaseWeapon및 WeaponDataAsset 작성함.
+ #### 오른쪽 이동 애님에이션을 미러데이터를 이용하여, 반전 시켜 좌측 이동 애니메이션으로 변경 및 적용함.
+ #### Weapon 스폰 구현함.

### 08-03
+ #### 플레이어 캐릭터 무기 장착 함수 구현
+ #### 스폰된 Weapon을 각 무기DataAsset에 저장된 HoldSokcet에 부착함
+ #### 플레이어가 키를 누르면 아래의 진행 방식을 통해 무기 장착 함수가 호출 됨
  + #### 1. 현재 플레이어가 무기를 장착했는지 CurrentWeapon변수를 통해 확인함.
  + #### 2. 무기를 선택함.
    + #### ㄴ 2-1 현재 무기를 장착 한 상태가 아니면, 누른 키에 맞는 WeaponType을 저장된 WeaponDataAsset 맵에서 찾아, 해당 무기를 CurrentWeapon에, DataAsset은 CurrentDataAsset에 저장함.
    + #### ㄴ 2-2 반대로 현재 무기를 장착한 상태면, 해당 무기를 HoldSocket에 부착하는 함수를 호출 함, 그 후 AnimNotify를 통해 CurrentWeapon와 CurrentDataAsset를 초기화 함.
  + #### 3. 선택한 무기의  CurrentDataAsset에서 EquipMontage를 통해 애니메이션 몽타주를 실행함.
    + #### ㄴ AnimNotify를 통해 HandSocket에 무기를 부착함

