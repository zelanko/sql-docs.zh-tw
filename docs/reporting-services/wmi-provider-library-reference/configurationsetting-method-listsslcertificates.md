---
title: "ListSSLCertificates 方法 (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: wmi-provider-library-reference
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: ListSSLCertificates method
ms.assetid: 88cd0936-b202-4ab8-90f2-d9c3f66d37f4
caps.latest.revision: "12"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 5fb7ce1a50f310d7d83114fbc02c4b6c596ac1c7
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="configurationsetting-method---listsslcertificates"></a>ConfigurationSetting 方法 - ListSSLCertificates
  傳回報表伺服器電腦上的憑證清單。  
  
## <a name="syntax"></a>語法  
  
```vb  
Public Sub CreateSSLCertificateBinding (ByRef CertificateHash() as String, _  
    ByRef CertName() as String, ByRef HostName() as String, ByRef Length as Int32, _   
    ByRef HRESULT as Int32)  
```  
  
```csharp  
public void ListSSLCertificates(out string[] CertificateHash,   
    out string[] CertName, out string[] Hostname, out Int32 length,   
    out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>參數  
 *CertificateHash[]*  
 [out] 憑證雜湊。  
  
 *CertName]*  
 [out] 憑證的名稱。  
  
 *HostName[]*  
 [out] 憑證的主機名稱。  
  
 *長度*  
 [out] 代表 *CertificateHash*、 *CertName* 和 *HostName* 陣列的長度。  
  
 *HRESULT*  
 [out] 指出呼叫成功或失敗的值。  
  
## <a name="return-value"></a>傳回值  
 傳回 *HRESULT* ，指出方法呼叫成功或失敗。 值為 0 表示方法呼叫成功。錯誤碼則表示呼叫不成功。  
  
## <a name="remarks"></a>備註  
  
## <a name="requirements"></a>需求  
 **命名空間：** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [MSReportServer_ConfigurationSetting 成員](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
