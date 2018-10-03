---
title: SqlServiceType 屬性 （SqlServiceAdvancedProperty 類別） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: reference
apiname:
- SqlServiceType Property (SqlServiceAdvancedProperty Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SqlServiceType property
ms.assetid: 20f1663a-9a14-4f14-8c1b-8aa133e272c3
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: c94868a081dacc9a34bd6ae84914847bf4e5a388
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47743666"
---
# <a name="sqlservicetype-property-sqlserviceadvancedproperty-class"></a>SqlServiceType 屬性 (SqlServiceAdvancedProperty 類別)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  取得與進階屬性相關之受管理服務的類型。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.SetBoolValue(NumValue)  
```  
  
## <a name="parts"></a>組件  
 *object*  
 代表進階屬性的 [SqlServiceAdvancedProperty 類別](../../../relational-databases/wmi-provider-configuration-classes/sqlserviceadvancedproperty-class/sqlserviceadvancedproperty-class.md) 物件。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 指定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服務類型的 uint32 值。  
  
## <a name="remarks"></a>備註  
 傳回值可以是下列其中一個：  
  
|類型|定義|  
|----------|----------------|  
|*1*|MSSQLSERVER 是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服務。|  
|*2*|SQLSERVERAGENT 是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 服務。|  
|*3*|MSFTESQL 是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 全文檢索搜尋引擎服務。|  
|*4*|MsDtsServer 是 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 服務。|  
|*5*|MSSQLServerOLAPService 是 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 服務。|  
|*6*|ReportServer 是 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 服務。|  
|*7*|SQLBrowser 是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Browser 服務。|  
  
## <a name="see-also"></a>另請參閱  
 [啟動及停止服務](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
