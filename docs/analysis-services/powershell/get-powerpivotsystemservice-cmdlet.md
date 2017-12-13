---
title: "Get-powerpivotsystemservice 指令程式 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 33231250-3880-4d75-936b-d70662a01855
caps.latest.revision: "9"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7210a93db11f4cbabe4b8b574d1945f932c2f31c
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="get-powerpivotsystemservice-cmdlet"></a>Get-PowerPivotSystemService 指令程式
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]傳回的全域屬性[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]伺服陣列中的系統服務物件。 

>[!NOTE] 
>這份文件可能包含過時的資訊和範例。 使用 Get-help cmdlet 取得最新。
  
 **適用於** ：SharePoint 2010 和 SharePoint 2013。  
  
## <a name="syntax"></a>語法  
  
```  
Get-PowerPivotSystemService [-Identity <PowerPivotMidTierServicePipeBind>] [<CommonParameters>]  
```  
  
## <a name="description"></a>說明  
 Get-PowerPivotSystemService Cmdlet 會傳回 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務物件的全域屬性。 每個伺服器陣列只有一個父物件，但是每個伺服器陣列中可以有多個在伺服器陣列中個別應用程式伺服器上執行的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務執行個體。 父物件顯示的伺服器陣列層級設定不因執行個體而改變。 如果伺服器陣列包含多個 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 安裝，逗號分隔的執行個體清單會指出伺服器陣列中有多少個 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務執行個體。  
  
## <a name="parameters"></a>參數  
  
### <a name="-identity-powerpivotmidtierservicepipebind"></a>識別\<PowerPivotMidTierServicePipeBind >  
 指定要取得的父物件。 此值必須是可在伺服器陣列中唯一識別物件的有效 GUID。  
  
|||  
|-|-|  
|必要項？|false|  
|位置？|0|  
|預設值||  
|接受管線輸入？|true|  
|接受萬用字元？|false|  
  
### <a name="commonparameters"></a>\<一般參數 >  
 這個指令程式支援一般參數：Verbose、Debug、ErrorAction、ErrorVariable、WarningAction、WarningVariable、OutBuffer 和 OutVariable。 如需詳細資訊，請參閱 [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825)。  
  
## <a name="inputs-and-outputs"></a>輸入和輸出  
 輸入類型是可透過管道傳送至指令程式的物件類型。 傳回類型是指令程式所傳回的物件類型。  
  
|||  
|-|-|  
|輸入|無。|  
|輸出|無。|  
  
## <a name="example-1"></a>範例 1  
  
```  
C:\PS>Get-PowerPivotSystemService  
```  
  
 此範例會傳回父物件的全域屬性，顯示伺服器陣列中所有 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 系統服務執行個體共用的屬性。  
  
  
