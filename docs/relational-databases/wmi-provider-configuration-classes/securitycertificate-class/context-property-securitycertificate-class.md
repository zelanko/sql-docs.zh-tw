---
title: 內容屬性 （SecurityCertificate 類別） |Microsoft 文件
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: wmi
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Context Property (SecurityCertificate Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- Context property
ms.assetid: 65dd737f-81ce-479e-8219-7b1b4d8f57c7
caps.latest.revision: 32
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 9e61bfebae75a2eef746c8edaed00c5761abeac8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="context-property-securitycertificate-class"></a>Context 屬性 (SecurityCertificate 類別)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  取得安全性憑證的內容。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.Context [= value]  
```  
  
## <a name="parts"></a>組件  
 *物件*  
 代表安全性憑證的 [SecurityCertificate 類別](../../../relational-databases/wmi-provider-configuration-classes/securitycertificate-class/securitycertificate-class.md) 物件。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 **Sint32**陣列值，指定安全性憑證的內容。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定伺服器網路通訊協定和網路程式庫](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
