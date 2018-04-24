---
title: sys.bandwidth_usage （SQL Azure 資料庫） |Microsoft 文件
ms.custom: ''
ms.date: 03/04/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- bandwidth_usage
- sys.bandwidth_usage
- bandwidth_usage_TSQL
- sys.bandwidth_usage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.bandwidth_usage
- bandwidth_usage
ms.assetid: 43ed8435-f059-4907-b5c0-193a258b394a
caps.latest.revision: 21
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: a1bea0110a1e1b26862e9d2b76b6362b6aaf2a53
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="sysbandwidthusage-azure-sql-database"></a>sys.bandwidth_usage (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  **注意： 這只適用於[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]V11。**  
  
 傳回每個資料庫中所使用的網路頻寬的相關資訊 **[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V11 邏輯伺服器**。 針對所指資料庫傳回的每一個資料列都會摘要說明在一小時內的單一使用方向和類別。  
  
 **這已被取代的[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]V12 邏輯伺服器。**  
  
 **Sys.bandwidth_usage**檢視包含下列資料行。  
  
|Column Name|Description|  
|-----------------|-----------------|  
|**time**|頻寬消耗的小時。 這個檢視中的資料列是以每小時為基礎。 例如，2009-09-19 02:00:00.000 表示頻寬是在 2009 年 9 月 19 日的上午 2:00  和 3:00 之間耗用。|  
|**database_name**|使用頻寬的資料庫名稱。|  
|**方向**|使用的頻寬類型，下列其中一個值：<br /><br /> 輸入： 資料移入[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。<br /><br /> 輸出： 資料移出的[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。|  
|**class**|使用的頻寬類別，下列其中一個值：<br />內部： 在 Azure 平台中移動的資料。<br />外部： Azure 平台移出的資料。<br /><br /> 這個類別在資料庫參與區域之間的連續複製關聯性時，才會傳回 ([!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)])。 If a given database does not participate in any continuous copy relationship, then “Interlink” rows are not returned. 如需詳細資訊，請參閱本主題稍後的＜備註＞一節。|  
|**time_period**|尖峰或 OffPeak 發生使用時的時間週期。 The Peak time is based on the region in which the server was created. 例如，如果伺服器是在 "US_Northwest" 區域中建立，則尖峰時間會定義為介於太平洋標準時間上午 10:00 到 和 06:00:00 執行報表， 之間。|  
|**數量**|使用的頻寬數量，以 KB 為單位。|  
  
## <a name="permissions"></a>Permissions  
 此檢視僅供以**主要**伺服器層級主體登入的資料庫。  
  
## <a name="remarks"></a>備註  
  
### <a name="external-and-internal-classes"></a>外部和內部類別  
 每個資料庫在指定時間內，使用**sys.bandwidth_usage**檢視會傳回資料列，顯示類別和方向的頻寬使用量。 下列範例說明所指資料庫可能會公開的資料。 在這個範例中，時間是 2012-04-21 17:00:00，發生在尖峰時段。 資料庫名稱為 Db1。 在此範例中， **sys.bandwidth_usage**已傳回為 Ingress 與 Egress 方向及 External 與 Internal 類別的所有四個組合的資料列，如下所示：  
  
|time|database_name|direction|class|time_period|quantity|  
|----------|--------------------|---------------|-----------|------------------|--------------|  
|2012-04-21 17:00:00|Db1|Ingress|External|Peak|66|  
|2012-04-21 17:00:00|Db1|Egress|External|Peak|741|  
|2012-04-21 17:00:00|Db1|Ingress|Internal|Peak|1052|  
|2012-04-21 17:00:00|Db1|Egress|內部|Peak|3525|  
  
### <a name="interpreting-data-direction-for-includessgeodrincludesssgeodr-mdmd"></a>解譯 [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)] 的資料方向  
 如果是 [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)]，頻寬使用量資料會同時在連續複製關聯性兩端的邏輯 master 資料庫中顯示。 所以，您必須從您要查詢的邏輯伺服器的角度解譯入口和出口方向指標。 例如，請考慮從來源伺服器傳送 1MB 資料至目標伺服器的複寫資料流。 在這種情況下，1MB 在來源伺服器上會計入傳送的總資料量中，而在目標伺服器上，1MB 會記錄為接收的資料。  
  
> [!NOTE]  
>  傳送的大量資料是依照使用者資料流程的方向，從來源伺服器傳送到目標伺服器。 不過，有些資料需朝其他方向傳送。  
  
  
