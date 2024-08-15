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
  + #### 현재 플레이어가 무기를 장착했는지 CurrentWeapon변수를 통해 확인함.
  + #### 현재 무기를 장착 한 상태가 아니면, 누른 키에 맞는 WeaponType을 저장된 WeaponDataAsset 맵에서 찾아, 해당 무기를 CurrentWeapon에, DataAsset은 CurrentDataAsset에 저장하고 장착 애니메이션을 출력함.
  + #### 반대로 현재 무기를 장착한 상태면, 이미 장착된 무기와 장착할 무기의 WeaponType을 비교함.
    + #### ㄴ 서로 다른 WeaponType이면 현재 무기를 HoldSocket에 부착 하고 위의 무기 장착 로직을 실행 함.
    + #### ㄴ 서로 같은 WeaponType이면 CurrentDataAsset에서 UnEquipMontage 애니메이션을 출력하고, AnimNotify를 통해 특정 지점에서 무기를 HoldSocket에 부착 하고 함수를 종료함.

### 08-04
  + #### 검 장착시 이동 애니메이션 변경함.
  + #### 블랜드 스페이스를 추가 작성하고, WeaponType을 애님블루프린트에서 확인하여 Type에 맞게 애니메이션을 재생 함.
    
### 08-05
  + #### 콤보공격 구현을 위해 애님몽타지와 PlayRate를 가지고 있는 ComboMontage구조체를 작성하고, DataAsset에 배열로 추가함.
  + #### 좌클릭 입력을 인식 받으면, CanAttack 을 False로 변경하고, 애니메이션을 출력함.
  + #### CanAttack이 False로 상태에서 추가로 입력을 받으면, AnimNotifyState에서 현재 콤보 입력 가능 구간인지 확인후, 콤보 입력 가능 구간이면 CanCombo를 True로 변경하여 다음 애니메이션을 출력함.

### 08-06
  + #### 점프공격 추가함.
  + #### 점프 중에 공격 키를 누르면 점프 공격이 나오도록 애님플루프린트에 스테이트 추가 및 개선함.

### 08-07
  + #### 현재 상태를 확인하기 위해 StateComponent 추가함.
  + #### 공격 시 일정 시간 동안 Collision프로파일을 변경하여 Overlap이벤트가 작동 되도록 구현함.
  + #### 델리게이트를 통해 WeaponComponent에서 호출하고, Collision은 AnimNotify를 이용하여 특정 구간에서만 Collision이 작동하도록 구현 함.

### 08-08
  + #### 공격 적중 시 피격 모션 출력
  + #### Damage를 준 객체와 맞은 객체의 Location을 통해 방향을 구하고, 해당 방향에 맞는 피격 몽타주를 재생 하도록 구현함.
  + #### State를 확인하여 Die 상태이면 사망 모션이 나오도록 구현함.

### 08-09
  + #### 데미지 처리 구현
  + #### 스탯의 최대와 현재 값을 가지고 있는 F_Stat구조체를 가지고, 해당 구조체를 각 스탯의 수량에 맞게 가지는 F_Status 구조체를 작성함.
  + #### DA_Status DataAsset를 작성하여 F_Status 구조체를 추가하고, 해당 DataAsset을 상속 받는 DA_Player를 작성함.
  + #### 해당 StatusComponent를 작성하여, StatusDataAsset을 추가하고, 초기화 및 수치 변화를 작성함.
  + #### 데미지를 받을 시 해당 StatusComponent의 ChangeStatus함수를 호출하여 현재 체력을 변경함.
  + #### 데미지를 중복해서 받는 현상을 DoOnce를 활용하여 해결 함.

### 08-10
  + #### 방어 상태 및 애니메이션 추가
  + #### 마우스 우클릭을 누르는동안 방어 애니메이션이 나오도록 구현함.
  + #### E_State에 막기상태, 공격 상태, 무기 장착중 상태, 무기 장착 해제중 상태를 추가함.
  + #### 현재 상태에서 가능한 행동만 작동 하도록 구현함

  + |상태|불가 행동|
    |:------:|:-------------|
    | 공격 |무기 장착 및 해제, 점프 및 점프 공격, 방어|
    | 방어 |공격, 무기 장착 및 해제, 점프|
    | 점프 |일반 공격, 방어|
    | 맞음 |공격, 무기 장착 및 해제, 방어, 점프|
    
### 08-11
  + #### 세키로식 패링 구현(가드 패링)

### 08-12
  + #### HP 및 스태미나 Bar 구현
  + #### 피격시 HP Bar 감소 구현

### 08-13
  + #### 스태미나 감소 구현(공격, 점프, 가드 시 감소)

### 08-14
  + #### 플레이어가 Hit상태이거나 Idle상태이면 Tick이벤트에서 스태미나를 지속적으로 회복하도록 구현함.
  + #### 가드 시 스태미나가 0이 되면 자세가 무너지는 애니메이션을 출력하면서, 일시적으로 스태미너 회복이 불가능한 Stun상태가 되도록 구현.
  + #### Stun상태에서는 점프 및 공격을 할수 없음.
  + #### 추가적으로 점프 후 바닥에 착지 시 스태미나가 회복 및 무기장착 및 장착 해제 상태에서도 스태미나가 회복 되도록 개선함.

### 08-15
  + #### 플레이어에 방패 부착
  + #### 가드 시 방패의 색상이 변경되어 시각적으로 알수있게 개선
