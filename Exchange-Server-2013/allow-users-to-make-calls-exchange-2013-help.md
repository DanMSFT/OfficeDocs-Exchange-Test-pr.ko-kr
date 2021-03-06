﻿---
title: '사용자가 전화를 걸 수 있도록: Exchange 2013 Help'
TOCTitle: 사용자가 전화를 걸 수 있도록
ms:assetid: b6e696ce-c848-475b-a598-9035677497e2
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb232172(v=EXCHG.150)
ms:contentKeyID: 51407735
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사용자가 전화를 걸 수 있도록

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2015-03-09_

*외부로 전화 걸기*는 Outlook Voice Access 번호를 사용하여 UM 다이얼 플랜을 호출한 다음 내부 또는 외부 전화 번호로 전화를 걸거나 통화를 전송할 때 사용하는 프로세스입니다. 통합 메시징에서는 여러 가지 외부로 전화 걸기 설정을 사용하여 전화를 겁니다. 외부로 전화 걸기를 구성하려면 UM(통합 메시징) 다이얼 플랜에 대해 전화 걸기 규칙, 전화 걸기 규칙 그룹 및 전화 걸기 권한 부여를 구성한 다음 UM 다이얼 플랜, UM 사서함 정책 및 자동 전화 교환에 대해 외부로 전화 걸기 권한을 부여해야 합니다. 또한 조직에서 외부로 전화 걸기를 제어할 수 있는 전화 걸기나 액세스 코드, 국가 번호 접두사, 국내/지역 또는 국제 번호 형식을 포함하도록 UM 다이얼 플랜을 구성할 수 있습니다. 이 항목에서는 전화 걸기 규칙, 전화 걸기 규칙 그룹 및 전화 걸기 권한 부여와 이러한 기능을 사용하여 조직의 외부로 전화 걸기를 제어하고 권한을 부여하는 방법에 대해 설명합니다.

**목차**

개요

Types of users

Outdialing settings

Configuring outdialing

Applying configured dialing rule groups

Applying dialing rules

## 개요

외부로 전화 걸기는 다음 상황에서 수행됩니다.

  - 외부 전화 번호로 전화를 걸 때

  - 자동 전화 교환으로 통화를 전송할 때

  - 조직의 사용자에게 통화를 전송할 때

  - UM 사용 가능 사용자가 전화에서 재생 기능을 사용할 때

외부로 전화 걸기가 제대로 작동하려면 다음 설정을 올바르게 구성해야 합니다.

  - **전화 걸기 규칙**   전화 걸기 규칙은 UM 사용 가능 사용자가 전화를 거는 번호와 PBX(Private Branch Exchange) 또는 IP PBX에서 전화를 거는 번호를 정의합니다.

  - **전화 걸기 그룹**   전화 걸기 그룹은 전화 걸기 그룹 내의 사용자가 걸 수 있는 전화 유형을 결정합니다.

  - **전화 걸기 권한 부여**   전화 걸기 권한 부여는 사용자가 불필요한 전화 요금을 발생시키거나 시외 전화를 걸지 못하게 하기 위해 적용하는 제한을 결정합니다.

다이얼 플랜 또는 자동 전화 교환을 호출하는 사용자에 대해 외부로 전화 걸기를 사용하도록 설정하려면 다음을 수행해야 합니다.

  - 다이얼 플랜과 연결된 UM IP 게이트웨이에서 표시하는 VoIP 게이트웨이가 발신 전화를 허용하는지 확인합니다.

  - UM 다이얼 플랜에 전화 걸기 규칙을 만들어 전화 걸기 규칙 그룹을 만듭니다.

  - UM IP 게이트웨이와 같은 다이얼 플랜에 연결된 UM 다이얼 플랜, UM 사서함 정책 또는 자동 전화 교환에 대해 국내/지역 및 국제 전화 걸기 규칙 그룹용 전화 걸기 권한 부여를 추가합니다.

## 사용자 유형

통합 메시징에서 외부로 전화 걸기 기능은 인증된 사용자와 인증되지 않은 사용자의 두 유형이 사용할 수 있습니다. UM 자동 전화 교환을 호출하는 모든 사용자는 인증되지 않은 사용자입니다. 사용자가 Outlook Voice Access 번호로 전화를 걸 때 내선 번호와 PIN을 제공하지 않고 사서함에 로그인하지 않았으므로 인증되지 않은 사용자로 간주됩니다. 내선 번호와 PIN을 제공하고 사서함에 로그인한 사용자는 인증됩니다.

사용자가 UM 다이얼 플랜에 구성된 Outlook Voice Access 번호로 전화를 건 다음 사서함에 로그인하지 않은 상태로 전화를 걸거나 통화를 전송하면 UM 다이얼 플랜 외부로 전화 걸기 설정만 통화에 적용됩니다. 익명 또는 인증되지 않은 사용자가 UM 자동 전화 교환에 전화를 걸면 자동 전화 교환에 구성된 외부로 전화 걸기 설정과 자동 전화 교환과 연결되어 있는 다이얼 플랜에 구성된 외부로 전화 걸기 설정이 해당 전화에 모두 적용됩니다.

다이얼 플랜에 구성되어 있는 Outlook Voice Access 번호로 전화를 걸어 사서함에 정상적으로 로그인하는 사용자는 인증된 사용자가 됩니다. 사용자가 인증되면 외부로 전화 걸기 전화 설정은 해당 사용자에게 연결된 UM 사서함 정책의 전화 걸기 규칙 및 전화 걸기 권한 부여 설정을 사용합니다.

맨 위로 이동

## 외부로 전화 걸기 설정

조직에 대해 외부로 전화 걸기 규칙을 적용하려면 여러 설정을 구성해야 합니다. 올바른 전화 걸기 규칙 및 전화 걸기 권한 부여를 사용하여 생성된 UM 다이얼 플랜, UM 자동 전화 교환 및 UM 사서함 정책을 구성해야 할 뿐 아니라, UM 다이얼 플랜에 대해 액세스 코드, 번호 접두사 및 번호 형식도 구성해야 합니다. 다음 전화 걸기 설정은 다이얼 플랜, 자동 전화 교환 및 UM 사서함 정책에 구성됩니다.

  - 외부 회선, 국가/지역 및 국가별 액세스 코드

  - 국가 번호 접두사

  - 국내/지역 및 국제 번호 형식

  - 구성된 국내/지역 및 국제 전화 걸기 규칙 그룹

  - 허용된 국내/지역 및 국제 전화 걸기 규칙 그룹

  - 전화 걸기 규칙 항목

  - 전화 걸기 권한 부여

조직에 대해 외부에서 전화 걸기를 올바르게 구성하려면 먼저 외부에서 전화 걸기에서 각 구성 요소를 사용하는 방법 및 구성 요소를 구성하는 방법을 이해해야 합니다. 다음 표에는 외부에서 전화 걸기가 올바르게 작동하도록 UM 다이얼 플랜, UM 자동 전화 교환 및 UM 사서함 정책에 대해 구성해야 하는 각 구성 요소가 나와 있습니다.

### 외부로 전화 걸기 구성 요소

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>구성 요소</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>전화 걸기 코드, 번호 접두사 및 번호 형식</p></td>
<td><p>UM에서는 전화 걸기 코드, 번호 접두사 및 번호 형식을 사용하여 발신 전화를 걸 올바른 번호를 확인합니다. 전화 걸기 코드, 번호 접두사 및 번호 형식을 구성하여 UM 다이얼 플랜과 연결된 UM 자동 전화 교환으로 전화를 걸거나 다이얼 플랜에 구성된 Outlook Voice Access 번호로 전화를 거는 사용자의 발신 전화를 제한할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>전화 걸기 규칙 그룹</p></td>
<td><p>전화 걸기 규칙 그룹은 발신 전화를 위해 전화 번호를 PBX로 보내기 전에 수정하기 위해 만듭니다. 전화 걸기 규칙 그룹은 UM에서 전화를 건 전화 번호에서 번호를 제거하거나 추가합니다. 예를 들어 외부 회선으로 액세스할 때 7자리 전화 번호에 9를 접두사로 자동 추가하도록 전화 걸기 규칙 그룹을 만들 수 있습니다. 이 예에서 발신 전화를 거는 사용자는 조직의 외부에 있는 사람에게 연결하기 위해 전화 번호 앞에 9를 누를 필요가 없습니다.</p>
<p>각 전화 걸기 규칙 그룹에는 전화 걸기 규칙 그룹 내의 사용자가 걸 수 있는 국내/지역 및 국제 전화의 유형을 결정하는 전화 걸기 규칙이 포함되어 있습니다. 전화 걸기 규칙 그룹은 UM 다이얼 플랜에 연결된 사용자나 UM 자동 전화 교환 및 UM 다이얼 플랜과 연결된 UM 사서함 정책에 적용됩니다. 각 전화 걸기 규칙 그룹에는 하나 이상의 전화 걸기 규칙이 있어야 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>전화 걸기 규칙 항목</p></td>
<td><p>전화 걸기 규칙은 전화 걸기 규칙 그룹 내에서 사용자가 걸 수 있는 전화의 유형을 결정할 때 사용됩니다. 전화 걸기 규칙 그룹을 만들 때 하나 이상의 전화 걸기 규칙을 구성합니다.</p>
<p>각 전화 걸기 규칙을 구성할 때는 전화 걸기 규칙 이름, 변환할 번호 패턴(<em>숫자 마스크</em>) 및 전화 건 번호를 입력해야 합니다. 또한 설명도 입력할 수 있습니다. 설명은 전화 걸기 규칙의 사용 방법을 설명하거나 전화 걸기 규칙이 적용되는 사용자 그룹을 설명하는 데 사용됩니다. 전화 걸기 규칙에 숫자 마스크와 전화 건 번호를 추가할 때는 전화 번호의 숫자를 x로 대체할 수 있습니다(예: 91425xxxxxxx). 별표(*) 기호를 와일드카드 문자로 사용할 수도 있습니다(예: 91425*).</p></td>
</tr>
<tr class="even">
<td><p>전화 걸기 권한 부여</p></td>
<td><p>전화 걸기 권한 부여에서는 전화 걸기 규칙 그룹을 사용하여 특정 UM 사서함 정책, 다이얼 플랜 또는 자동 전화 교환과 연결된 사용자에게 전화 걸기 제한을 적용합니다. 이 제한을 사용하여 사용자가 국내/지역 또는 국제 전화 번호로 전화를 거는 것을 허용할 수도 있습니다.</p>
<p>UM 다이얼 플랜에 대해 전화 걸기 규칙을 만든 후 UM 사서함 정책, 다이얼 플랜 또는 자동 전화 교환에 전화 걸기 규칙 그룹을 추가합니다. UM 사서함 정책에 전화 걸기 규칙 그룹을 추가하고 나면 정의된 모든 설정이나 규칙이 UM 사서함 정책과 연결된 UM 사용 가능 사용자에게 적용됩니다.</p></td>
</tr>
</tbody>
</table>


맨 위로 이동

## 외부로 전화 걸기 구성

전화 걸기 규칙 그룹은 UM 다이얼 플랜에 구성된 전화 걸기 규칙 하나 이상의 모음입니다. UM 다이얼 플랜에는 국내/지역 및 국제의 두 가지 유형의 전화 걸기 규칙 그룹을 구성할 수 있습니다. 국내/지역 전화 걸기 규칙 그룹은 동일한 국가나 지역 내에서 전화를 건 전화 번호에 적용됩니다. 국제 전화 걸기 규칙 그룹은 한 국가나 지역에서 다른 국가나 지역으로 건 국제 전화 번호에 적용됩니다.

각 UM 다이얼 플랜에는 하나 이상의 전화 걸기 규칙 그룹을 포함할 수 있습니다. 사용자 집합에 전화 걸기 규칙 그룹을 적용하려면 전화 걸기 규칙 그룹을 만든 후 UM 다이얼 플랜 및 해당 UM 다이얼 플랜과 연결된 UM 자동 전화 교환/UM 사서함 정책에 대해 허용되는 전화 걸기 규칙 그룹 목록에 추가해야 합니다.

전화 걸기 규칙 그룹을 사용하여 특정 범주에 속한 UM 사용 가능 사용자 그룹에 적용할 전화 걸기 규칙을 지정할 수 있습니다. 예를 들어 전화 걸기 규칙 그룹을 사용하여 국제 전화를 걸 수 있는 사용자 그룹과 국내 또는 시내 전화만 걸 수 있는 그룹을 지정할 수 있습니다. EAC(Exchange 관리 센터)를 사용하거나 Exchange 관리 셸에서 **Set-UMDialPlan** cmdlet을 사용하여 전화 걸기 규칙 그룹을 만들 수 있습니다. 전화 걸기 규칙 그룹을 만들 때는 그룹에 대해 전화 걸기 규칙을 하나 이상 정의해야 합니다.

사용자가 특정 전화 번호로 전화를 걸면 UM이 번호를 가져와 전화 걸기 규칙에서 일치하는 항목을 찾습니다. 일치하는 항목이 있으면 UM은 전화 걸기 규칙을 사용하여 해당 규칙의 **전화 건 번호** 섹션에 나열된 전화 번호나 숫자를 확인해 전화를 걸 번호를 결정합니다. 전화 걸기 규칙의 **전화 건 번호** 상자에 나와 있는 번호로 전화를 겁니다.

다음 표에서는 전화 걸기 규칙 그룹 및 전화 걸기 규칙의 예를 보여줍니다. 이 예에서 시내 전화 전용 및 국내 전화 전용은 이미 만든 전화 걸기 규칙 그룹입니다. 시내 전화 전용이라는 전화 걸기 규칙 그룹에는 91425\* 및 91206\*의 전화 걸기 규칙 두 개가 있으며 국내 전화 전용에도 91509\* 및 91360\*의 전화 걸기 규칙 두 개가 있습니다.

### 전화 걸기 규칙 그룹 및 전화 걸기 규칙

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>이름</th>
<th>NumberMask</th>
<th>DialedNumber</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>시내 전화 전용</p></td>
<td><p>91425*</p></td>
<td><p>91*</p></td>
<td><p>시내 전화</p></td>
</tr>
<tr class="even">
<td><p>시내 전화 전용</p></td>
<td><p>91206*</p></td>
<td><p>91*</p></td>
<td><p>시내 전화</p></td>
</tr>
<tr class="odd">
<td><p>국내 전화 전용</p></td>
<td><p>91509*</p></td>
<td><p>9*</p></td>
<td><p>국내 전화</p></td>
</tr>
<tr class="even">
<td><p>국내 전화 전용</p></td>
<td><p>91360*</p></td>
<td><p>9*</p></td>
<td><p>국내 전화</p></td>
</tr>
</tbody>
</table>


예를 들어 사용자가 9-1-425-555-1234로 전화를 걸면 UM은 4255551234로 전화를 겁니다. 즉, UM은 숫자가 아닌 문자(이 예에서는 하이픈)를 빼고 전화 걸기 규칙의 숫자 마스크를 적용합니다. 이 예에서 UM은 숫자 마스크 91\*를 적용합니다. 즉, UM은 9나 1을 빼고 숫자 1 오른쪽에 표시된 다른 모든 전화 번호로만 전화를 겁니다. 여기에는 별표(\*)로 표시된 모든 숫자가 포함됩니다.

EAC 또는 셸을 사용하여 하나 또는 여러 개의 국내/지역 및 국제 전화 걸기 규칙 그룹과 전화 걸기 규칙을 만들고 구성할 수 있습니다. 전화 걸기 규칙 그룹과 전화 걸기 규칙을 여러 개 만들거나 복잡하게 만드는 경우 셸에서 쉼표로 구분된 값(.csv) 파일을 사용할 수 있습니다. 전화 걸기 규칙 그룹 및 전화 걸기 규칙의 목록을 가져오거나 내보낼 수 있습니다.

.csv 파일에 정의한 전화 걸기 규칙 그룹 및 전화 걸기 규칙의 목록을 가져오려면 다음과 같이 **Set-UMDialPlan** cmdlet을 실행합니다.

    Set-UMDialPlan "MyUMDialPlan" -ConfiguredInCountryOrRegionGroups $(IMPORT-CSV c:\dialrules\InCountryRegion.csv)

UM 다이얼 플랜에 구성된 전화 걸기 규칙 그룹의 목록을 검색하려면 다음과 같이 **Get-UMDialPlan** cmdlet을 실행합니다.

    (Get-UMDialPlan -id "MyUMDialPlan").ConfiguredInCountryOrRegionGroups | EXPORT-CSV C:\incountryorregion.csv

.csv 파일은 올바른 형식으로 만들고 저장해야 합니다. .csv 파일의 각 줄은 하나의 전화 걸기 규칙을 나타냅니다. 그러나 각 전화 걸기 규칙은 동일한 전화 걸기 규칙 그룹에 구성됩니다. 파일의 각 규칙에는 쉼표로 구분된 네 개의 섹션이 있습니다. 이 섹션은 이름, 숫자 마스크, 전화 건 번호 및 설명입니다. 각 섹션은 필수 사항으로 설명 섹션을 제외한 각 섹션에 올바른 정보를 입력해야 합니다. 다음 섹션에서 텍스트 항목과 쉼표 사이에는 공백이 없어야 하며 규칙 사이 또는 끝에도 빈 줄이 없어야 합니다. 다음은 국내/지역 전화 걸기 규칙 그룹과 전화 걸기 규칙을 만드는 데 사용할 수 있는 .csv 파일의 예입니다.

**Name,NumberMask,DialedNumber,Comment**

**Low-rate,91425xxxxxxx,9xxxxxxx,Local call**

**Low-rate,9425xxxxxxx,9xxxxxxx,Local call**

**Low-rate,9xxxxxxx,9xxxxxxx,Local call**

**Any,91\*,91\*,Open access to in-country/region numbers**

**Long-distance,91408\*,91408\*,long distance**

다음은 국제 전화 걸기 규칙 그룹과 전화 걸기 규칙 항목을 만드는 데 사용할 수 있는 .csv 파일의 예입니다.

**Name,NumberMask,DialedNumber,Comment**

**International, 901144\*, 901144\*, international call**

**International, 901133\*, 901133\*, international call**

맨 위로 이동

## 구성된 전화 걸기 규칙 그룹 적용

전화 걸기 규칙 그룹은 UM 다이얼 플랜에 생성됩니다. EAC 또는 셸에서 **Set-UMDialPlan** cmdlet을 사용하여 국내/지역 또는 국제 전화 걸기 규칙 그룹을 만들 수 있습니다. UM 다이얼 플랜에 적절한 전화 걸기 규칙 그룹을 만들고 전화 걸기 규칙을 정의한 후에는 만든 전화 걸기 규칙 그룹을 사용자가 음성 메일 시스템에 액세스하는 방법에 따라 UM 다이얼 플랜, UM 자동 전화 교환 또는 UM 사서함 정책과 연결된 사용자에게 적용할 수 있습니다.

다음은 UM 다이얼 플랜에 만든 전화 걸기 규칙 그룹을 적용할 수 있는 대상입니다.

  - **동일한 다이얼 플랜**   사서함에 로그인하지 않는 상태로 Outlook Voice Access 번호로 전화를 거는 모든 사용자에게 설정이 적용됩니다. `MyAllowedDialRuleGroup`이라는 국내/지역 전화 걸기 규칙 그룹을 동일한 다이얼 플랜에 적용하려면 셸 **Set-UMDialPlan** cmdlet을 다음과 같이 사용합니다.
    
        Set-UMDialPlan -Identity MyUMDialPlan -AllowedInCountryOrRegionGroups MyAllowedDialRuleGroup

  - **하나 또는 여러 개의 UM 사서함 정책   **UM 사서함 정책에 구성된 설정이 해당 UM 사서함 정책과 연결된 모든 사용자에게 적용됩니다. UM 사서함 정책에 구성되는 설정은 사서함에 로그인한 상태로 Outlook Voice Access 번호로 전화를 거는 사용자에게 적용됩니다. `MyAllowedDialRuleGroup`이라는 국내/지역 전화 걸기 규칙 그룹을 하나의 UM 사서함 정책에 적용하려면 EAC에서 UM 사서함 정책의 **전화 걸기 권한 부여** 페이지를 사용하거나 다음과 같이 셸에서 **Set-UMMailboxPolicy** cmdlet을 사용합니다.
    
        Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -AllowedInCountryOrRegionGroups MyAllowedDialRuleGroup

  - **UM 다이얼 플랜과 연결된 하나 또는 여러 개의 자동 전화 교환   **이 설정은 UM 자동 전화 교환을 호출하는 모든 사용자에게 적용됩니다. `MyAllowedDialRuleGroup`이라는 국내/지역 전화 걸기 규칙 그룹을 하나의 UM 자동 전화 교환에 적용하려면 EAC에서 자동 전화 교환의 **전화 걸기 권한 부여** 페이지를 사용하거나 다음과 같이 셸에서 **Set-UMAutoAttendant** cmdlet을 사용합니다.
    
        Set-UMAutoAttendant -Identity MyUMAutoAttendant -AllowedInCountryOrRegionGroups MyAllowedDialRuleGroup

다음 표에서는 통합 메시징에 전화 걸기 규칙 그룹을 적용하는 방법을 요약해서 보여줍니다.

### 외부로 전화 걸기 규칙 적용

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>전화 건 사람 유형</th>
<th>범위</th>
<th>적용된 외부로 전화 걸기 설정</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook Voice Access 번호</p></td>
<td><p>다이얼 플랜 Outlook Voice Access 번호로 전화를 걸고 사서함에 로그인함</p></td>
<td><p>UM 사서함 정책</p></td>
</tr>
<tr class="even">
<td><p>익명의 전화 건 사람</p></td>
<td><p>다이얼 플랜 Outlook Voice Access 번호로 전화를 검</p></td>
<td><p>UM 다이얼 플랜</p></td>
</tr>
<tr class="odd">
<td><p>익명의 전화 건 사람</p></td>
<td><p>자동 전화 교환 파일럿 또는 내선 번호로 전화를 검</p></td>
<td><p>UM 자동 전화 교환</p></td>
</tr>
<tr class="even">
<td><p>조직 내부에서 전화 건 사람</p></td>
<td><p>전화에서 재생 번호로 전화를 검</p></td>
<td><p>UM 사서함 정책</p></td>
</tr>
</tbody>
</table>


맨 위로 이동

## 전화 걸기 규칙 적용

외부로 전화 걸기 프로세스는 다음 상황에서 수행됩니다.

  - 통합 메시징에서 발신자를 위해 외부 전화 번호로 전화할 때

  - 통합 메시징에서가 자동 전화 교환으로 통화를 전송할 때

  - 통합 메시징에서 조직의 사용자에게 통화를 전송할 때

  - UM 사용 가능 사용자가 전화에서 재생 기능을 사용할 때

각각의 외부로 전화 걸기 시나리오에서 UM은 구성된 전화 걸기 규칙을 적용한 다음 사용자를 위해 전화를 겁니다. 그러나 시나리오와 사용자가 통화를 시작하는 방법에 따라 UM이 전화를 걸고 있는 전화 번호에 전화 걸기 규칙의 일부만 적용할 수도 있습니다. UM이 전화를 걸고 있는 전화 번호에 구성된 모든 외부로 전화 걸기 규칙을 적용하는 기타 외부로 전화 걸기 시나리오도 있습니다.

맨 위로 이동

