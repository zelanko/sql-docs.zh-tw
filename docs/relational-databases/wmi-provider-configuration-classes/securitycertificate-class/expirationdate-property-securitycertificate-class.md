---
title: ExpirationDate 屬性 （SecurityCertificate 類別） |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
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
- ExpirationDate Property (SecurityCertificate Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ExpirationDate property
ms.assetid: b7fbb9e9-85c1-475b-8e49-7c82fb3740aa
caps.latest.revision: 33
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: feae08ebe9171e3b9fb2896a892b23eec880bffe
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="expirationdate-property-securitycertificate-class"></a>ExpirationDate 屬性 (SecurityCertificate 類別)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  取得安全性憑證停止生效的日期。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.ExpirationDate [= value]  
```  
  
## <a name="parts"></a>組件  
 *物件*  
 代表安全性憑證的 [SecurityCertificate 類別](../../../relational-databases/wmi-provider-configuration-classes/securitycertificate-class/securitycertificate-class.md) 物件。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 A **uint32**值，指定安全性憑證的到期日。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱  
 [設定伺服器網路通訊協定和網路程式庫](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
