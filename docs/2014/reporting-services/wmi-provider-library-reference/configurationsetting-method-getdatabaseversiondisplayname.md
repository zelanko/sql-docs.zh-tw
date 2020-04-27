---
title: GetDatabaseVersionDisplayName 方法 (WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- GetDatabaseVersionDisplayName method
ms.assetid: e1286424-7043-4f12-a7ad-1cf69e81baa4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 05ee617f1a065c44a7c593af244d778f76a7a627
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66098412"
---
# <a name="getdatabaseversiondisplayname-method-wmi"></a>GetDatabaseVersionDisplayName 方法 (WMI)
  取得給定報表伺服器資料庫版本字串的顯示名稱。  
  
## <a name="syntax"></a>語法  
  
```vb  
Public Sub GetDatabaseVersionDisplayName(Version As String, DisplayName As String, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void GetDatabaseVersionDisplayName(string Version, string DisplayName, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>參數  
 *版本*  
 包含報表伺服器資料庫之版本字串的字串。  
  
 *DisplayName*  
 [out] 包含對應至所提供版本之顯示名稱的字串。  
  
 *HRESULT*  
 [out] 指出呼叫成功或失敗的值。  
  
## <a name="remarks"></a>備註  
 下表將顯示資料庫版本與顯示字串的對應。  
  
|**版本**|`Version`|**顯示名稱**|  
|-----------------|-----------------|----------------------|  
|RS 2005 SP2|@DBVersion = 'C.0.8.54'|SQL Server 2005 SP2|  
|RS 2005 SP1|@DBVersion = 'C.0.8.43'|SQL Server 2005 SP1|  
|RS 2005 RTM|@DBVersion = 'C.0.8.40'|SQL Server 2005|  
|RS 2000 SP2|@DBVersion = 'C.0.6.54'|SQL Server 2000 SP2|  
|RS 2000 SP1|@DBVersion = 'C.0.6.51'|SQL Server 2000 SP1|  
|RS 2000 RTM|@DBVersion = 'C.0.6.43'|SQL Server 2000|  
|Hotfix||最接近的適用版本|  
  
 若為 *2000 之前的* Version [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，就會傳回 ACT_E_BAD_VERSION 的 HRESULT。  
  
## <a name="return-value"></a>傳回值  
 傳回 *HRESULT* ，指出方法呼叫成功或失敗。 值為 0 表示方法呼叫成功。 非零值則表示已發生錯誤。  
  
## <a name="requirements"></a>需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_ConfigurationSetting 成員](msreportserver-configurationsetting-members.md)  
  
  
