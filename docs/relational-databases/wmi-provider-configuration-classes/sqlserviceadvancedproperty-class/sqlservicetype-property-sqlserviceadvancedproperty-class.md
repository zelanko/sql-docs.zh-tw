---
description: SqlServiceType 屬性 (SqlServiceAdvancedProperty 類別)
title: 'SqlServiceType 屬性 (SqlServiceAdvancedProperty) '
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
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
ms.openlocfilehash: 70260b9b24e3f71e84e986c48a5a4a6b58d5446c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88485023"
---
# <a name="sqlservicetype-property-sqlserviceadvancedproperty-class"></a>SqlServiceType 屬性 (SqlServiceAdvancedProperty 類別)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
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
|*8*|Nsservice.exe 是 [!INCLUDE[ssNoVersion](../../../includes/ssns-md.md)] 通知服務。|  
|*9*|MSSQLFDLauncher 是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 全文檢索篩選背景程式啟動器服務。|  
|*10*|SQLPBENGINE 是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Polybase 引擎服務。|  
|*11*|SQLPBDMS 是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Polybase 資料移動服務。|  
|*12*|MSSQLLaunchpad 是啟動控制 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 板服務。|  
  
## <a name="see-also"></a>另請參閱  
 [啟動及停止服務](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
