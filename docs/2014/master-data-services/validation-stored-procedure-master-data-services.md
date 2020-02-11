---
title: 驗證預存程序 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 332d3c86-4440-4f12-a6cb-ffbfbccde52c
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 89e0b57501eb948d0c67a6dc0a055051b7d19b18
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "65481334"
---
# <a name="validation-stored-procedure-master-data-services"></a>驗證預存程序 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，驗證版本，以便將商務規則套用到模型版本中的所有成員。  
  
 本主題說明如何使用 **mdm.udpValidateModel** 預存程序來驗證資料。 如果您是 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 應用程式的管理員，可以改用使用者介面來進行驗證。 如需詳細資訊，請參閱 [根據商務規則驗證版本 &#40;Master Data Services&#41;](validate-a-version-against-business-rules-master-data-services.md)。  
  
> [!NOTE]  
>  如果您在暫存處理序完成之前，即叫用驗證，則不會驗證尚未完成暫存的成員。  
  
## <a name="example"></a>範例  
  
```  
DECLARE @ModelName nVarchar(50) = 'Customer'   
DECLARE @Model_id int   
DECLARE @UserName nvarchar(50)= 'DOMAIN\user_name'   
DECLARE @User_ID int   
DECLARE @Version_ID int   
  
SET @User_ID = (SELECT ID    
                 FROM mdm.tblUser u   
                 WHERE u.UserName = @UserName)   
SET @Model_ID = (SELECT Top 1 Model_ID   
                 FROM mdm.viw_SYSTEM_SCHEMA_VERSION   
                 WHERE Model_Name = @ModelName)   
SET @Version_ID = (SELECT MAX(ID)   
                 FROM mdm.viw_SYSTEM_SCHEMA_VERSION   
                 WHERE Model_ID = @Model_ID)  
  
EXECUTE mdm.udpValidateModel @User_ID, @Model_ID, @Version_ID, 1  
  
```  
  
## <a name="parameters"></a>參數  
 此處理序的參數如下：  
  
|參數|描述|  
|---------------|-----------------|  
|UserID|使用者識別碼。|  
|Model_ID|模型識別碼。|  
|Version_ID|版本識別碼。|  
  
## <a name="see-also"></a>另請參閱  
 [資料匯入 &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)   
 [根據商務規則驗證版本 &#40;Master Data Services&#41;](validate-a-version-against-business-rules-master-data-services.md)  
  
  
