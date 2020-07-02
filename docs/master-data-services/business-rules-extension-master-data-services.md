---
title: Business Rules Extension
description: 您可以套用使用者定義的 SQL 腳本，做為 Master Data Services 中預先定義之商務規則條件和動作的延伸模組。
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 4c18be5f-a3fa-45a8-9be6-0f45f58bbc9e
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: c4d6ad76f68acb72072f04728e55793bad3aa9cd
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85813669"
---
# <a name="business-rules-extension-master-data-services"></a>商務規則延伸模組 (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，您可以套用使用者定義的 SQL 指令碼，以做為預先定義之條件與動作的擴充功能。  
  
> [!NOTE]  
>  所有的指令碼必須在 [usr] 結構描述下定義。  
  
 符合下列準則的 SQL 函數可用來當作商務規則條件。  
  
-   傳回值類型必須為 BIT。  
  
-   參數類型只支援下列類型。  
  
    -   NVARCHAR  
  
    -   DATETIME2  
  
    -   DECIMAL (有效位數，小數位數)  
  
         有效位數必須是 38  
  
         小數位數必須是從 0 到 7 的值  
  
 使用下列語法的 SQL 預存程序可用來當作商務規則動作  
  
```  
CREATE PROCEDURE [usr].[YourAction]  
       (         
            @MemberIdList mdm.[MemberId] READONLY,  
            @ModelName NVARCHAR(MAX),  
            @VersionName NVARCHAR(MAX),  
            @EntityName NVARCHAR(MAX),  
            @BusinessRuleName NVARCHAR(MAX)  
        )    
      AS BEGIN    
       ...     
       END  
  
```  
  
 使用者定義的指令碼不會加入部署封裝中。 部署封裝之前，請確定目標 Master Data Services 資料庫包含商務規則中所使用的所有指令碼。  
  
 會以 mds_br_user 身分執行指令碼動作，該身分具有下列權限  
  
|||  
|-|-|  
|**結構描述**|**權限**|  
|mdm|SELECT|  
|stg|SELECT、UPDATE、DELETE、EXECUTE、INSERT|  
|usr|FULL|  
  
## <a name="prerequisites"></a>必要條件  
 若要執行此程序：  
  
-   您必須擁有存取系統管理功能區域的權限。  
  
-   您必須是模型管理員。 如需詳細資訊，請參閱[管理員 &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)  
  
-   使用者定義指令碼已加入 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 資料庫中。  
  
## <a name="create-a-business-rule-to-take-a-user-defined-script-as-a-condition-or-as-an-action"></a>建立商務規則，採用使用者定義指令碼作為條件或動作  
  
1.  在主資料管理員中，按一下 [系統管理] ****。  
  
2.  從功能表列，指向 [管理] **** ，然後按一下 [商務規則] ****。  
  
3.  在 [商務規則]**** 頁面上，從 [模型]**** 下拉式清單選取模型。  
  
4.  從 [實體] **** 下拉式清單選取實體。  
  
5.  從 [成員類型] **** 下拉式清單中，選取要套用商務規則的成員類型。  
  
6.  按一下 **[新增]** 。  
  
7.  依下列方式來建立使用者定義指令碼作為條件。  
  
    1.  在 [如果] **** 區塊下，按一下 [加入] **** 按鈕。 面板隨即顯示。  
  
    2.  從 [運算子]**** 下拉式清單中，選取 [使用者定義的指令碼]**** 下的使用者定義函數。  
  
    3.  會顯示使用者定義函數的所有參數。  
  
    4.  將值指派給每個參數  
  
    5.  按一下 [檔案] 。  
  
8.  依下列方式來採用使用者定義指令碼作為動作。  
  
    1.  在 [然後] **** 區塊下，按一下 [加入] **** 按鈕。 面板隨即顯示。  
  
    2.  從 [運算子]**** 下拉式清單中，選取 [使用者定義的指令碼]**** 下的使用者定義函數。  
  
    3.  按一下 [檔案] 。  
  
## <a name="see-also"></a>另請參閱  
 [商務規則 &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)   
 [商務規則條件 &#40;Master Data Services&#41;](../master-data-services/business-rule-conditions-master-data-services.md)   
 [商務規則動作 &#40;Master Data Services&#41;](../master-data-services/business-rule-actions-master-data-services.md)  
  
  
