﻿---
title: '원본 위치 유지 및 소송 보존: Exchange 2013 Help'
TOCTitle: 원본 위치 유지 및 소송 보존
ms:assetid: 71031c06-852d-44d8-b558-dff444eaef8c
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ff637980(v=EXCHG.150)
ms:contentKeyID: 50483349
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 원본 위치 유지 및 소송 보존

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2017-11-15_


> [!NOTE]
> Exchange Online(Office 365 및 Exchange Online 독립 실행형 계획)에 새 원본 위치 유지 만들기에 대한 마감 날짜인 2017년 7월 1일을 연기했습니다. 하지만 올해 말 또는 내년 초에는 Exchange Online에 새 원본 위치 유지를 만들 수 없습니다. 원본 위치 유지를 사용하는 대신, Office 365 보안 및 준수 센터의 <A href="https://go.microsoft.com/fwlink/?linkid=780738">eDiscovery 사례</A> 또는 <A href="https://go.microsoft.com/fwlink/?linkid=827811">보존 정책</A>을 사용할 수 있습니다. 새 원본 위치 유지를 해제한 후에도 기존 원본 위치 유지를 계속 수정할 수 있으며 Exchange Server 2013 및 Exchange 하이브리드 배포에서 새 원본 위치 유지를 계속 만들 수 있습니다. 또한 사서함을 소송 보존 상태로 계속 유지할 수 있습니다.



소송 가능성이 존재하는 경우 조직은 해당 사례와 관련된 전자 메일을 비롯한 ESI(전자적으로 저장된 정보)를 보존해야 합니다. 이러한 가능성은 사례의 세부 사항이 알려지기 전에 발생하기도 하며 대부분 보존 범위가 넓습니다. 조직에서는 특정 항목과 관련된 모든 전자 메일 또는 특정 개인의 모든 전자 메일을 보존해야 합니다. 조직의 eDiscovery(Electronic Discovery) 방식에 따라 전자 메일을 보존하기 위해 채택할 수 있는 방법은 다음과 같습니다.

  - 최종 사용자에게 메시지를 삭제하지 않도록 요청하여 전자 메일을 보존할 수 있습니다. 그러나 사용자가 의도적으로 또는 우연히 전자 메일을 삭제할 가능성이 여전히 있습니다.

  - MRM(메시징 레코드 관리)과 같은 자동 삭제 메커니즘을 일시 중단할 수 있습니다. 이 경우 사용자 사서함에 많은 양의 전자 메일이 쌓여 사용자의 생산성에 영향을 미칠 수 있습니다. 또한 자동 삭제를 일시 중단해도 사용자가 수동으로 전자 메일을 삭제하는 것은 차단되지 않습니다.

  - 일부 조직에서는 전자 메일을 보관함으로 복사 또는 이동하여 삭제, 변경 또는 변조되지 않도록 합니다. 이 경우 메시지를 보관함으로 복사 또는 이동하는 데 필요한 수동 작업, 또는 Microsoft Exchange 외부에서 전자 메일을 수집 및 저장하는 데 사용되는 타사 제품으로 인해 비용이 증가됩니다.

전자 메일을 보존하지 않으면 조직은 조직의 레코드 보존 및 검색 프로세스에 대한 조사, 불리한 법정 판결, 처벌 또는 벌금과 같은 법적, 금전적 위험에 노출될 수 있습니다.

원본 위치 유지 또는 소송 보존으로 설정 다음과 같은 목표를 수행 하기 위해 사용할 수 있습니다.

  - 전체 사용자 사서함에 보존 하 고 사서함 항목을 보존 합니다.

  - 사용자나 MRM과 같은 자동 삭제 프로세스에 의해 삭제 된 사서함 항목을 보존 합니다.

  - 쿼리 기반 원본 위치 유지를 사용하여 지정된 조건과 일치하는 항목 검색 및 보존

  - 항목을 무기한 또는 일정 기간 동안 보존합니다.

  - 각 사례 또는 조사용으로 사용자에게 여러 보존 상태를 적용합니다.

  - MRM을 일시 중단할 필요 없이으로 사용자에 게 투명 하 게 보관 하는 유지 됩니다.

  - 사용 하도록 설정에서 원본 위치 eDiscovery 검색에 배치 되는 항목의 보존 합니다.

**목차**

In-Place Hold scenarios

원본 위치 유지 및 소송 보존

Placing a mailbox on In-Place Hold

보류에 공용 폴더를 배치합니다.

보류 및 복구 가능한 항목 폴더

보류 및 사서함 할당량

보류 및 전자 메일 전달을

Preserving archived Lync content

보류에서 사서함을 삭제합니다.

Office 365에 Exchange 2013에서 마이그레이션 사서함에 유지

## 원본 위치 유지 시나리오

Exchange Server 2010에서 법적 보유라는 개념은 사용자의 모든 사서함 데이터를 무기한으로 또는 보유가 없어질 때까지 보존하는 것을 의미합니다. Exchange 2013에서는 원본 위치 유지에 다음과 같은 매개 변수를 지정할 수 있는 새로운 보존 모델이 도입되었습니다.

  - **유지 해야하는 작업**   키워드, 보낸사람 및 받는 사람, 예: 쿼리 매개 변수를 사용 하 여 유지 하는 항목 시작 및 종료 날짜, 및 전자 메일 메시지와 같은 메시지 종류를 지정할 수도 지정할 수 또는 일정 항목에 배치 하려는 유지 합니다.

  - **보존 기간**   항목 보존 기간을 지정할 수 있습니다.

새 모델인 이 원본 위치 유지 기능을 사용하면 다음과 같은 시나리오에서 사서함 항목을 보존하기 위한 세분화된 보존 정책을 만들 수 있습니다.

  - **무기한 보존**   무기한 보존 설정 시나리오 소송 보존으로 설정 하는 것과 비슷합니다. EDiscovery 요구 사항을 충족할 수 있도록 사서함 항목을 보존 하기 위한는 것입니다. 소송 보존 또는 조사 기간 동안 항목은 삭제 되지 않습니다. 기간 종료 날짜 없음 구성 되어 있으므로 사전에 알려져 있지 않습니다. 모든 메일 항목을 보관할 무기한, 쿼리 매개 변수를 지정 하거나 하지 기간 시간을 유지 하는 위치를 만들 때 합니다.

  - **쿼리 기반 보존**   조직에서 지정된 쿼리 매개 변수를 기반으로 항목을 보존하는 경우 쿼리 기반 원본 위치 유지를 사용할 수 있습니다. 키워드, 시작 및 종료 날짜, 보낸 사람 및 받는 사람 주소, 메시지 유형과 같은 쿼리 매개 변수를 지정할 수 있습니다. 쿼리 기반 원본 위치 유지를 만들고 나면 쿼리 매개 변수와 일치하는 기존의 모든 사서함 항목과 이후에 생성되는 사서함 항목이 보존됩니다.
    

    > [!IMPORTANT]
    > 항목을 검색할 수 없는 것으로 표시 된 일반적으로 첨부 파일을 색인을 실패를 보존 됩니다 쿼리 매개 변수를 일치 하는지 여부를 결정할 수 없으므로 합니다. 검색할 수 없는 항목에 대 한 자세한 내용은 <A href="unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md">Exchange eDiscovery의 검색할 수 없는 항목</A>을 참조 하십시오.



  - **시간 기반 보존**   원본 위치 유지 및 소송 보존으로 설정 모두 허용 시간 항목을 보관할 기간을 지정할 수 있습니다. 사서함 항목을 받거나 만든 날짜에서 기간 계산 됩니다.
    
    조직에서 모든 사서함 항목을 특정 기간(예: 7년) 동안 보존해야 하는 경우 시간 기반 보존 기능을 만들 수 있습니다. Exchange 2013에서는 보존 항목에 대한 보존 기간을 지정할 수 있습니다. 보존 상태의 항목은 수신된 날짜를 기반으로 기간이 계산됩니다. 예를 들어, 시간 기반 원본 위치 유지 상태인 사서함의 보존 기간이 365일로 설정되었다고 가정해 봅니다. 해당 사서함의 항목이 수신된 날짜로부터 300일 후에 삭제되는 경우 영구적으로 삭제되기 전까지 65일 동안 추가로 보존됩니다. 시간 기반 원본 위치 유지를 보존 정책과 함께 사용하면 항목을 지정된 기간 동안 보존하다가 해당 기간 이후에 영구적으로 제거할 수 있습니다.

사용자에 게 여러 보존 시키려면 원본 위치 유지를 사용할 수 있습니다. 사용자에 게 여러 보존 놓으면 모든 쿼리 기반 보류에서 검색 쿼리는 함께 ( **OR** 연산자). 이 경우 모든 쿼리 기반 사서함에 배치 하는 보류에 키워드의 최대 수는 500입니다. 500 명이 넘는 키워드 다음 사서함에 있는 모든 콘텐츠가 없는 경우 (뿐아니라 검색 조건과 일치 하는 콘텐츠) 대기 상태로 설정 됩니다. 모든 콘텐츠는 키워드의 총 수는 500 개를 감소 또는 때까지 유지 됩니다.

맨위로 돌아가기

## 원본 위치 유지 및 소송 보존

소송 보존, eDiscovery에 대 한 데이터를 유지 하기 위해 Exchange 2010 도입 된 보류 기능 Exchange 2013 에서 계속 제공 됩니다. 소송 보존 사서함의 **LitigationHoldEnabled** 속성을 사용합니다. 세분화 된 원본 위치 유지를 제공 하는 반면 쿼리 매개 변수 및 여러를 배치 하는 기능에 따라 기능을 포함 하 고, 보류에서 모든 항목을 배치할 수만 허용 소송 보존 합니다. 사서함이 소송 보존으로 설정 중일 때 항목을 저장할 까지의 기간을 지정할 수도 있습니다. 사서함 항목을 받거나 만든 날짜에서 기간 계산 됩니다. 기간으로 설정 되지 않은 경우 무기한 또는 보존이 제거 될 때까지 항목이 유지 됩니다.

사서함에 게 동시에 하나 이상의 원본 위치 유지 및 소송 보존으로 설정 (하지 않고 기간 동안)에 배치 되 면 때 무기한 유지 제거 될 때까지 또는 항목을 모두 보관 됩니다. 소송 보존을 제거 하는 경우 사용자가 원본 위치 유지 상태로 하나 이상의 배치 여전히 In-place Hold 조건과 일치 하는 항목 보류 설정에 지정 된 기간에 대 한 보관 됩니다. Exchange 2010 소송 보존 설정을 적용 하려면, 계속, Exchange 2013 사서함 서버로에서 소송 보존으로 설정에 해당 준수 보장 하는 동안 요구 사항이 충족 되는 사서함을 이동할 때 및 이동 후 합니다.


> [!NOTE]
> 원본 위치 유지 또는 소송 보존으로 설정 된 사서함을 할 때 보류 주 및 보관 사서함 모두에 배치 됩니다. Exchange 하이브리드 배포에서 온-프레미스에서 기본 사서함 보류를 배치 하는 경우 클라우드 기반 보관 사서함 (활성화 된 경우)도 대기 상태로 설정 됩니다.



자세한 내용은 다음을 참조하십시오.

  - [전체 사서함에 소송 보존으로 설정](place-a-mailbox-on-litigation-hold-exchange-2013-help.md)

  - [모든 사서함을 보류](place-all-mailboxes-on-hold-exchange-2013-help.md)

## 사서함을 원본 위치 유지 상태로 설정

[검색 관리](discovery-management-exchange-2013-help.md) RBAC(역할 기반 액세스 제어) 역할 그룹에 추가되었거나 법적 보유 및 사서함 검색 관리 역할이 할당된 권한 있는 사용자는 사서함 사용자를 원본 위치 유지 상태로 설정할 수 있습니다. 레코드 관리자, 준수 관리자 또는 조직 법무 부서의 변호사에게 최소 권한을 할당하여 작업을 위임할 수 있습니다. 검색 관리 역할 그룹 할당에 대한 자세한 내용은 [Exchange eDiscovery 사용 권한 할당](assign-ediscovery-permissions-in-exchange-exchange-2013-help.md)를 참조하십시오.


> [!IMPORTANT]
> Exchange 2010, 법적 보존 역할 사서함에 소송 보존으로 설정 하는 충분 한 사용 권한 가진 사용자를 제공 합니다. Exchange 2013 사서함에는 무기한 또는 시간 기반 원본 위치에 보존 하려면 동일한 권한을 사용할 수 있습니다. 그러나 한 쿼리 기반 원본 위치 유지를 만들려면 사용자 역할을 할당 해야는 사서함 검색 합니다. 검색 관리 역할 그룹에 할당 한 이러한 역할에 있습니다.



Exchange 2013에서는 원본 위치 유지 기능이 원본 위치 eDiscovery 검색과 통합되어 있습니다. EAC(Exchange 관리 센터)의 **원본 eDiscovery 및 유지** 마법사나 Exchange 관리 셸의 **New-MailboxSearch** 및 관련 cmdlet을 사용하여 사서함을 원본 위치 유지 상태로 설정할 수 있습니다. 사서함을 원본 위치 유지 상태로 설정하는 방법에 대한 자세한 내용은 [만들기 또는 In-place Hold 제거](create-or-remove-an-in-place-hold-exchange-2013-help.md)를 참조하십시오.


> [!NOTE]
> 온-프레미스 사서함에 대 한 클라우드 기반 보관 파일을 프로 비전 하려면 Exchange Online 보관을 사용 하는 경우 관리 해야 원본 위치 유지 온-프레미스 Exchange 2013 조직에서. 디렉터리 동기화를 사용 하 여 클라우드 기반 보관 사서함으로 설정이 자동 전파를 보관 합니다. 앞서 설명한 것 처럼 온-프레미스 사서함을 보류에 넣을 때 해당 클라우드 기반 보관도 대기 상태로 설정 됩니다.



많은 조직에서는 사용자가 유지 상태로 설정될 경우 이를 사용자에게 알려야 합니다. 또한 사서함이 보존 상태인 경우 사서함 사용자에게 적용 가능한 보존 정책을 일시 중단할 필요가 없습니다. 메시지가 계속 예상대로 삭제되므로 사용자는 자신이 보존 상태임을 인식하지 못할 수 있습니다. 조직에서 보존 상태가 된 사용자에게 이를 알려야 하는 경우 사서함 사용자의 **Retention Comment** 속성에 알림 메시지를 추가하고 **RetentionUrl** 속성을 사용하여 추가 정보가 있는 웹 페이지에 연결합니다. Outlook 2010 이상에서는 Backstage 영역에 이 알림을 표시합니다. 사서함에 대한 이러한 속성을 추가하고 관리하려면 셸을 사용해야 합니다.

맨위로 돌아가기

## 보류에 공용 폴더를 배치합니다.

Exchange Online 원본 위치 유지를 사용 하 여 보류 중인 공용 폴더를 배치할 수 있습니다. 소송 보존을 사용 하 여 공용 폴더에 대 한 지원 되지 않습니다. In-place Hold를 만들 때는 조직에서 모든 공용 폴더에 보류를 배치 하는 옵션만 합니다. 모든 공용 폴더 사서함에는 원본 위치 유지 배치 되도록이 반환이 됩니다.

또한 원본 위치 유지에 공용 폴더를 추가할 때 공용 폴더 계층 구조 동기화 프로세스와 관련 된 전자 메일 메시지 유지 됩니다. 이 다양 한 계층 구조에서에서 발생할 수 있습니다 동기화 관련 전자 메일 항목 보존 되 고 있습니다. 이러한 메시지는 공용 폴더 사서함에서 복구 가능한 항목 폴더에 대 한 저장소 할당량을 채울 수 있습니다. 이 방지 하려면 수는 쿼리 기반 원본 위치 유지 만들고 검색 쿼리를 다음 `property:value` 쌍을 추가 합니다.

    NOT(subject:HierarchySync*)

결과 제목줄에 "HierarchySync"에 배치 되지 않습니다 구가 포함 된 메시지 (공용 폴더 계층 구조 동기화와 관련 된)를 저장 합니다.

## 보류 및 복구 가능한 항목 폴더

원본 위치 유지 및 소송 보존으로 설정 항목을 유지 하려면 복구 가능한 항목 폴더를 사용 합니다. 비공식적 이라고 하는 기능을 대체 하는 복구 가능한 항목 폴더의 *휴지통*Exchange 의 이전 버전입니다. 복구 가능한 항목 폴더 Outlook, Outlook Web App 및 다른 전자 메일 클라이언트의 기본 보기에서 숨겨져 있습니다. 복구 가능한 항목 폴더에 대 한 자세한 내용은, [복구 가능한 항목 폴더](recoverable-items-folder-exchange-2013-help.md)를 참조 하십시오.

사용자가 지운 편지함 폴더 이외의 폴더에서 메시지를 삭제하면 해당 메시지는 기본적으로 지운 편지함 폴더로 이동됩니다. 이를 *이동*이라고 합니다. 사용자가 항목을 *일시 삭제*하거나(Shift와 Delete 키를 눌러서 실행) 지운 편지함 폴더에서 항목을 삭제하면 해당 메시지가 복구할 수 있는 항목 폴더로 이동되고 그로 인해 사용자 보기에서 사라지게 됩니다.

복구 가능한 항목 폴더의 항목은 사용자의 사서함 데이터베이스에 구성 된 삭제 된 항목 보존 기간에 대 한 보관 됩니다. 기본적으로 삭제 된 항목 보존 기간을 사서함 데이터베이스에 대 한 14 일로 설정 됩니다. 복구 가능한 항목 폴더에 대 한 저장소 할당량을 구성할 수도 있습니다. 이 조직 잠재적 거부 복구 가능한 항목 폴더 및 사서함 데이터베이스의 신속 하 게 성장으로 인해 DoS (서비스) 공격에서에서 보호 됩니다. 사서함의 원본 위치 유지 또는 소송 보존에 배치 되지, 하는 경우 항목 비워집니다 영구적으로, 처음에 복구 가능한 항목 폴더에서 처음으로 수행 복구 가능한 항목 경고 보내기 할당량을 초과 하는 또는 항목에 긴 기간에 대 한 폴더에 내 상주 하는 경우 보다 삭제 된 항목 보존 기간입니다.

복구 가능한 항목 폴더에는 다양 한 사이트의 삭제 된 항목을 저장 하 고 원본 위치 유지 및 소송 보존을 용이 하 게 하는 데 사용 하는 다음과 같은 하위 포함 됩니다.

  - **Deletions**   지운 편지함 폴더에서 제거되거나 다른 폴더에서 일시 삭제된 항목은 삭제 하위 폴더로 이동되며, Outlook 및 Outlook Web App에서 지운 편지함 복구 기능을 사용할 때 사용자에게 표시됩니다. 기본적으로 항목은 사서함 데이터베이스 또는 사서함에 대해 구성된 삭제된 항목 보존 기간이 만료될 때까지 이 폴더에 존재합니다.

  - **제거**   때 사용자 항목 복구 가능한 항목 폴더에서 (사용 하 여 삭제는 지운 편지함 복구 도구 Outlook 및 Outlook Web App, 항목에서 제거 폴더로 이동 되었습니다. 사서함 데이터베이스 또는 사서함에 구성 된 삭제 된 항목 보존 기간을 초과 하는 항목도 제거 폴더로 이동 됩니다. 이 폴더에 있는 항목이 지운 편지함 복구 도구를 사용 하는 경우 사용자에 게 표시 되지 않습니다. 사서함 도우미는 사서함을 처리할 때 제거 폴더의 항목은 사서함 데이터베이스에서 제거 됩니다. 사서함 도우미 소송 보존으로 설정에 사서함 사용자를 추가할 때이 폴더의 항목을 제거 하지 않고 합니다.

  - **DiscoveryHold**   사용자가 원본 위치 유지 상태로 설정되면 삭제된 항목이 이 폴더로 이동됩니다. 사서함 도우미는 사서함을 처리할 때 이 폴더의 메시지를 평가합니다. 원본 위치 유지 쿼리와 일치하는 항목은 쿼리에 지정된 보존 기간에 도달할 때까지 유지됩니다. 보존 기간이 지정되지 않은 경우에는 항목이 무기한으로 또는 사용자가 보존 상태에서 제거될 때까지 보존됩니다.

  - **버전**   사용자의 원본 위치 유지 또는 소송 보존으로 설정에 놓으면 사서함 항목 변조 또는 수정 보호 하 여 사용자 또는 프로세스에 의해 되어야 합니다. 이 작업은 *기록 중 복사* 프로세스를 사용 하 여 수행 됩니다. 사용자 또는 사서함 항목의 프로세스 변경 된 특정 속성에 변경 내용이 커밋되기 전에 원본 항목의 복사본을 버전 폴더에 저장 됩니다. 이후 변경 내용에 대 한이 프로세스가 반복 됩니다. 항목 버전 폴더에 캡처된도 인덱싱되고 원본 위치 eDiscovery 검색에서 반환 합니다. 보류를 제거한 후에 관리 되는 폴더 도우미에 의해 버전 폴더에 복사본 제거 됩니다.

### COW(기록 중 복사)를 트리거하는 속성

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>항목 종류</th>
<th>COW(기록 중 복사)를 트리거하는 속성</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>메시지(IPM.Note*)</p>
<p>게시물(IPM.Post*)</p></td>
<td><ul>
<li><p>제목</p></li>
<li><p>본문</p></li>
<li><p>첨부 파일</p></li>
<li><p>보낸 사람/받는 사람</p></li>
<li><p>보낸/받은 날짜</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>메시지 및 게시물 외의 항목</p></td>
<td><p>다음을 제외한 표시되는 속성에 대한 변경:</p>
<ul>
<li><p>항목 위치(항목이 다른 폴더로 이동될 경우)</p></li>
<li><p>항목 상태 변경(읽음 또는 읽지 않음)</p></li>
<li><p>항목에 적용된 보존 태그 변경</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>기본 폴더 임시 보관함의 항목</p></td>
<td><p>없음(임시 보관함 폴더의 항목은 COW(기록 중 복사)에서 제외됨)</p></td>
</tr>
</tbody>
</table>



> [!IMPORTANT]
> 참석자로부터 모임 응답이 수신되고 모임에 대한 추적 정보가 업데이트되면 모임 이끌이의 사서함에서 일정 항목에 대해 COW(기록 중 복사) 기능을 사용할 수 없게 됩니다. 미리 알림 집합이 있는 항목과 일정 항목의 경우에는 ReminderTime 및 ReminderSignalTime 속성에 대해 COW(기록 중 복사)를 사용하지 않도록 설정되어 있습니다. 이들 속성에 대한 변경 내용은 COW(기록 중 복사)에서 캡처되지 않습니다. RSS 피드에 대한 변경 내용은 COW(기록 중 복사)에서 캡처되지 않습니다.



DiscoveryHold, 제거, 및 버전 폴더는 사용자에 게 보이지 않지만 복구 가능한 항목 폴더의 모든 항목 Exchange 검색을 통해 인덱싱되 및 원본 위치 eDiscovery를 사용 하 여 검색할 수는 있습니다. 사서함 사용자는 원본 위치 유지 또는 소송 보존으로 설정에서 제거 되 면 후 DiscoveryHold, 제거, 및 버전 폴더의 항목은 관리 되는 폴더 도우미에 의해 제거 됩니다.

맨위로 돌아가기

## 보류 및 사서함 할당량

복구 가능한 항목 폴더의 항목 사용자의 사서함 할당량 계산 되지 않습니다. Exchange 복구 가능한 항목 폴더에는 자체의 할당량 합니다. Exchange 대 한 *RecoverableItemsWarningQuota* 및 *RecoverableItemsQuota* 사서함 속성의 기본값은는 20GB 및 30GB 각각 설정 합니다. Exchange Server 2013 에 대 한 사서함 데이터베이스에 대 한 이러한 값을 수정 하려면 [Set-MailboxDatabase](https://technet.microsoft.com/ko-kr/library/bb123971\(v=exchg.150\)) cmdlet을 사용 합니다. 개별 사서함에 대 한 수정, [Set-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123981\(v=exchg.150\)) cmdlet을 사용 합니다.

사용자의 복구 가능한 항목 폴더 ( *RecoverableItemsWarningQuota* 매개 변수에 의해 지정 된) 대로 복구할 수 있는 항목에 대 한 경고 할당량을 초과 하면 사서함 서버의 응용 프로그램 이벤트 로그에 이벤트가 기록 됩니다. 폴더 ( *RecoverableItemsQuota* 매개 변수에 의해 지정 된) 대로 복구할 수 있는 항목에 대 한 할당량을 초과 하면 사용자는 지운 편지함 폴더 비우기 또는 사서함 항목을 영구적으로 삭제 수 없습니다. 또한 기록 중 복사는 수정 된 항목의 복사본을 만들 수 없습니다. 따라서 것은 원본 위치 유지에 배치 하는 사서함 사용자에 대 한 복구 가능한 항목 할당량을 모니터링 하는 중요 합니다.

사용자의 기본 사서함) (에서 복구 가능한 항목 폴더에 대 한 할당량 Exchange Online 자동으로 원본 위치 유지 또는 소송 보존으로 설정 된 사서함을 할 때 100GB로 증가 되었습니다. 대기 사서함의 주 사서함의 복구 가능한 항목 폴더에 대 한 저장소 할당량 제한을 초과한 도달에 근접 한 경우에 다음과 같은 작업을 수행할 수 있습니다.

  - **보관 사서함을 사용 하도록 설정 하 고 자동 확장 보관 설정**   복구 가능한 항목 폴더에 대 한 사용 하 여 무제한 저장 용량이 보관 사서함을 사용 하도록 설정 하 고 다음 켜서 자동 확장 보관 기능에서 Exchange Online 하 여 설정할 수 있습니다. 이 기본 사서함과 사용자의 보관에서 복구할 수 있는 항목 폴더에 대 한 저장 용량에 무제한 금액의 복구 가능한 항목 폴더에 100GB에서 만들어집니다. 참조 방법: [Office 365 보안 및 규정 준수 센터에서 사서함 보관 사용](https://go.microsoft.com/fwlink/p/?linkid=863320) 및 [Office 365에서 무제한 보관을 사용](https://go.microsoft.com/fwlink/p/?linkid=844569)합니다.
    
    **참고**:
    
      - 수동으로 이동 되도록 만료 된 항목의 사서함을 처리 하는 데 길잡이 트리거하는 관리 되는 폴더 도우미가 실행 해야할 복구 가능한 항목 폴더에 대 한 저장소 할당량을 초과 하면 되는 사서함에 대 한 보관을 활성화 한 후의 보관 사서함의 복구 가능한 항목 폴더입니다. 자세한 내용은 [사서함에 대 한 할당량 대기 복구 가능한 항목을 증가](https://go.microsoft.com/fwlink/p/?linkid=786479)에서 4 단계를 참조 하십시오.
    
      - 사용자의 사서함에 있는 다른 항목이 새로운 보관 사서함으로 이동되었을 수 있다는 점에 유의하시기 바랍니다. 보관 사서함을 사용하도록 설정한 다음 이러한 현상이 발생할 수 있다고 사용자에게 말하는 방안을 고려해 보세요.

  - **보관 사서함에 대 한 사용자 지정 보존 정책 만들기**    보관 사서함을 사용 하도록 설정 하 고 자동 확장 원본 위치 유지 또는 소송 보존으로 설정에 있는 사서함에 대 한 보관, 외에도 보류에 사서함에 대 한 사용자 지정 보존 정책을 만들 수도 있습니다. 이 보겠습니다 정책을 적용 하면 보존 대기 대기 되지 않은 사서함에 적용 되는 기본 MRM 정책와에서는 다른 사서함에 있습니다. 이 보류에 있는 사서함에 대 한 특별히 설계 된 보존 태그를 적용할 수 있습니다. 복구 가능한 항목 폴더에 대 한 새 보존 태그 만들기 (영문) 포함 됩니다.

자세한 내용은 [사서함에 대 한 할당량 대기 복구 가능한 항목을 증가](https://go.microsoft.com/fwlink/p/?linkid=786479)을 참조 하십시오.

## 보류 및 전자 메일 전달을

사용자는 자신의 사서함에 대 한 착신 전환 하는 전자 메일을 설정 하려면 Outlook 및 Outlook Web App 를 사용할 수 있습니다. 전자 메일 전달을 사용자에 게를 자신의 사서함에 또는 조직 외부에 있는 다른 사서함을 자신의 사서함에 전송 된 정방향 전자 메일 메시지를 구성할 수 있습니다. 전자 메일 전달은 원래 사서함으로 보낸 모든 메시지는 해당 사서함에 복사 되지 않습니다 하 고 전달 주소로 보내집니다 있도록 구성할 수 있습니다.

사서함에 대 한 전자 메일 전달을 설정 하는 경우 메시지를 원본 사서함으로 복사 되지 않습니다 어떻게 사서함이 대기 하는 경우 됩니까? 동작이 Exchange 2013 또는 Exchange Online 조직에 사서함이 있는지 여부에 따라 달라 집니다.

  - **Exchange Online**    사서함에 대 한 보존 설정은 배달 프로세스 동안 되는지 여부를 확인 합니다. 메시지는 사서함에 대 한 보류 기준을 충족 하는 경우 메시지의 복사본 복구 가능한 항목 폴더에 저장 됩니다. 즉, 다른 사서함에 전달 된 메시지를 찾으려면 원본 사서함을 검색 하려면 원본 위치 eDiscovery를 사용할 수 있습니다.

  - **Exchange 2013**    메시지는 다른 사서함에 전달 하 고 원본 사서함에 복사 되지, 하는 경우 되지 캡처한 있으며 복구 가능한 항목 폴더에 복사 합니다. 의미 전달 메시지는 원본 위치 eDiscovery 검색에서 반환 되지 않습니다. 이 문제를 해결 하기 위해 사용자가 전자 메일 전달을 구성 하는 기능이 제거 Exchange 2013 조직이 고려할 수 있습니다.

맨위로 돌아가기

## 보관된 Lync 콘텐츠 보존

Exchange 2013, Microsoft Lync 2013 및 Microsoft SharePoint 2013에서는 서로 다른 여러 데이터 저장소에서 항목을 보존하고 검색할 수 있는 통합된 보존 및 eDiscovery 환경을 제공합니다. Exchange 2013에서는 Lync Server 2013 콘텐츠를 Exchange에 보관할 수 있으므로 개별 SQL Server 데이터베이스를 보관된 Lync 콘텐츠에 저장할 필요가 없습니다. SharePoint 2013의 통합 보존 및 eDiscovery 기능을 사용하면 단일 콘솔에서 모든 저장소에 있는 데이터를 보존하고 검색할 수 있습니다.

원본 위치 유지 또는 소송 보존으로 설정에 Exchange 2013 사서함을 할 때 Microsoft Lync 2013 콘텐츠 (예: 인스턴트 메시징 대화 및 온라인 모임에서 공유 하는 파일)의 사서함에 보관 됩니다. Microsoft SharePoint 2013 에서 eDiscovery 센터 또는 Exchange 2013 에서 원본 위치 eDiscovery를 사용 하 여 사서함을 검색 하는 경우 검색 쿼리와 일치 하는 모든 보관 된 Lync 콘텐츠 검색 결과에 반환 됩니다. 또한 사서함에 보관 된 Lync 콘텐츠 검색을 제한할 수 있습니다.

Lync 콘텐츠를 Exchange 2013 사서함에 보관하려면 Exchange 2013과 Lync 2013의 통합을 구성해야 합니다. 자세한 내용은 다음 항목을 참조하십시오.

  - [보관에 대 한 계획](https://technet.microsoft.com/en-us/library/jj205069\(v=ocs.15\))

  - [보관 배포](https://technet.microsoft.com/en-us/library/jj205147\(v=ocs.15\))

맨위로 돌아가기

## 보류에서 사서함을 삭제합니다.

여부에 따라 결과 서로 다른 원본 위치 유지 또는 소송 보존으로 설정에 배치 되는 사서함을 삭제 하는 경우 Exchange 2013 또는 Exchange Online 조직에서 사서함입니다.

  - **Exchange 2013**    사서함을 보유 하는 사용자 계정을 삭제 하는 관리자, 사서함 사용자 계정에 연결 되어있지 않습니다 해당 사서함을 삭제 하도록 표시, 사서함의 경우에 유지 하는 Exchange 정보 저장소 검색 결국 것입니다. 사서함을 유지 하려는 경우 다음을 수행 해야 합니다.
    
    1.  사용자 계정을 삭제 하는 대신 사용자 계정을 사용 하지 않도록 설정 합니다.
    
    2.  해당 사용을 제한 하 고 사서함에 액세스 하는 사서함의 속성을 변경 합니다. 예, 집합 보내고 할당량 1, 사서함에 액세스할 수 있는 사용자 제한 및 사서함에 메시지를 보낼 수 있는 블록으로 받습니다.
    
    3.  데이터는 유지 더이상 필요 하거나 모든 데이터를 expunged 되었는지, 될 때까지 사서함을 유지 합니다.

  - **Exchange Online**    사용자의 사서함에서 원본 위치 유지 또는 소송 보존에 배치 되는 경우 해당 하는 Office 365 계정을 삭제 됩니다 사서함은 *비활성 사서함*, 즉 일시 삭제 된 사서함의 형식으로 변환 됩니다. 비활성 사서함은 조직에서 탈퇴 한 후 사용자 사서함의 내용을 유지 하기 위해 사용 됩니다. 비활성 사서함의 항목은 비활성 적용 되기 전에 사서함에 배치 된 보류의 기간에 대 한 유지 됩니다. 이렇게 하면 관리자, 규정 준수 관리자 또는 레코드 관리자를 사용 하 여 원본 위치 eDiscovery에 액세스 하 고 비활성 사서함의 내용을 검색 합니다. 비활성 사서함 전자 메일을 수신할 수 없음 및 조직의 공유 주소록 또는 다른 목록에 표시 되지 않습니다. 자세한 내용은 [Exchange Online에서 비활성 사서함](https://technet.microsoft.com/ko-kr/library/dn798632\(v=exchg.150\))을 참조 하십시오.

맨위로 돌아가기

## Office 365에 Exchange 2013에서 마이그레이션 사서함에 유지

Exchange 하이브리드 배포를가 이동 하면 (온보드)를 온-프레미스 Exchange 2013 사서함 Exchange OnlineOffice 365 에서 다음과 같은 조건이 적용 됩니다.

  - 원본 위치 유지 또는 소송 보존으로 설정에서 온-프레미스 사서함이 있는 경우 Exchange Online 에 사서함을 이동한 후 보류 설정이 유지 됩니다.

  - 원본 위치 유지 또는 소송 보존으로 설정에서 온-프레미스 사서함이 있는 경우의 복구 가능한 항목 폴더의 모든 콘텐츠 Exchange Online 사서함으로 이동 됩니다.


> [!NOTE]
> 설정 및 콘텐츠 유지 (영문)의 복구 가능한 항목 폴더는 조직 (offboard) 하 여 온-프레미스 Exchange 2013 를 Exchange Online 사서함을 이동 하는 경우에 보존 됩니다.



단계적 Exchange 마이그레이션 또는 단독형 Exchange 마이그레이션을 사용하는 등의 다른 방법으로 온-프레미스 전자 메일 데이터를 Office 365로 마이그레이션할 수 있습니다.

  - 단계적 마이그레이션을 사용하면 사서함을 Exchange 2003 또는 Exchange 2007에서 Office 365로 마이그레이션할 수 있습니다. 이러한 Exchange 버전에는 복구 가능한 항목 폴더와 해당 기능이 없습니다. 따라서 Exchange 2003 또는 Exchange 2007 사서함을 Office 365로 마이그레이션할 때는 이동할 복구 가능한 항목 폴더 콘텐츠가 없습니다.

  - 단독형 마이그레이션을 사용하면 사서함을 Exchange 2003, Exchange 2007, Exchange 2010에서 Office 365로 마이그레이션할 수 있습니다. 앞에서 설명한 것처럼 Exchange 2003 및 Exchange 2007 사서함에는 마이그레이션할 수 있는 복구 가능한 항목 폴더가 없습니다. 항목 복구 폴더는 Exchange 2010에서 도입되었으므로 단독형 마이그레이션을 사용하여 Exchange 2010 사서함을 마이그레이션하면 복구 가능한 항목 폴더의 콘텐츠가 Office 365로 마이그레이션됩니다.


> [!TIP]
> Exchange 2013 및 Exchange 2010Exchange 하이브리드 배포를는 것이 좋습니다 Office 365 를 온-프레미스 사서함을 마이그레이션할 수 있습니다.



맨위로 돌아가기

