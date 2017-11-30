---
title: "DeleteEncryptedInformation 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
apiname: DeleteEncryptedInformation (WMI MSReportServer_ConfigurationSetting Class)
apilocation: reportingservices.mof
apitype: MOFDef
helpviewer_keywords: DeleteEncryptedInformation method
ms.assetid: c14ed187-bdd9-4304-88e3-72072f03c21b
caps.latest.revision: "19"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 09025d87ac3684fa6cbd7bdf36c24bfaa74b307a
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="configurationsetting-method---deleteencryptedinformation"></a>ConfigurationSetting 方法 - DeleteEncryptedInformation
  從報表伺服器資料庫中刪除加密的資訊。  
  
## <a name="syntax"></a>語法  
  
```vb  
Public Sub DeleteEncryptedInformation(ByRef HRESULT As Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void DeleteEncryptedInformation(out Int32 HRESULT, out string[] ExtendedErrors);  
```  
  
## <a name="parameters"></a>參數  
 *HRESULT*  
 [out] 指出呼叫成功或失敗的值。  
  
 *ExtendedErrors[]*  
 [out] 包含呼叫所傳回之其他錯誤的字串陣列。  
  
## <a name="return-value"></a>傳回值  
 傳回 *HRESULT* ，指出方法呼叫成功或失敗。 值為 0 表示方法呼叫成功。 非零值則表示已發生錯誤。  
  
## <a name="remarks"></a>備註  
 叫用這個方法時，就會刪除下列資料：  
  
-   已加密的資料來源資訊，包括使用者名稱和密碼。  
  
-   使用傳遞延伸模組介面加密的訂閱資料。  
  
-   來自報表伺服器資料庫中索引鍵資料表的所有資訊。  
  
 叫用這個方法之後，使用者必須初始化使用報表伺服器資料庫的每部電腦。  
  
 呼叫 DeleteEncryptedInformation 方法並不會影響報表伺服器組態檔。  
  
## <a name="requirements"></a>需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_ConfigurationSetting 成員](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
