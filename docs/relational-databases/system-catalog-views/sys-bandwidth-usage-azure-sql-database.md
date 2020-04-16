---
title: 系統bandwidth_usage(Azure SQL 資料庫) |微軟文件
ms.custom: ''
ms.date: 01/28/2019
ms.service: sql-database
ms.reviewer: ''
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
author: julieMSFT
ms.author: jrasnick
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: ea963c07a15cd5c2db3cca113680026d3100936b
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/15/2020
ms.locfileid: "67942570"
---
# <a name="sysbandwidth_usage-azure-sql-database"></a>sys.bandwidth_usage (Azure SQL Database)

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

> [!NOTE]
> 這僅適用於[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]V11。  
  
 返回有關**[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]V11 資料庫伺服器**中每個資料庫使用的網路頻寬的資訊。 針對所指資料庫傳回的每一個資料列都會摘要說明在一小時內的單一使用方向和類別。  
  
 **這在 中已棄[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]用 。**  
  
 **sys.bandwidth_usage**視圖包含以下列。  
  
|資料行名稱|描述|  
|-----------------|-----------------|  
|**time**|頻寬消耗的小時。 這個檢視中的資料列是以每小時為基礎。 例如，2009-09-19 02:00:00.000 表示頻寬是在 2009 年 9 月 19 日的上午 2:00  和 3:00 之間耗用。|  
|**database_name**|使用頻寬的資料庫名稱。|  
|**方向**|使用的頻寬類型，下列其中一個值：<br /><br /> 進入:正在進入的[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]資料 。<br /><br /> 出口:正在移出的[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]資料 。|  
|**class**|使用的頻寬類別，下列其中一個值：<br />內部:在 Azure 平台內移動的數據。<br />外部:從 Azure 平台移出的數據。<br /><br /> 這個類別只會在資料庫參與區域 ([!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)]) 之間的連續複製關聯性時傳回。 如果給定資料庫不參與任何連續複製關係,則不返回"Interlink"行。 如需詳細資訊，請參閱本主題後面的＜備註＞一節。|  
|**time_period**|發生使用時的時間週期為 Peak 或 OffPeak。 The Peak time is based on the region in which the server was created. 例如，如果伺服器是在 "US_Northwest" 區域中建立，則尖峰時間會定義為介於太平洋標準時間上午 10:00 到 和 06:00:00 執行報表， 之間。|  
|**quantity**|使用的頻寬數量，以 KB 為單位。|  
  
## <a name="permissions"></a>權限

 此檢視僅在**主**資料庫中對伺服器級主體登錄可用。  
  
## <a name="remarks"></a>備註  
  
### <a name="external-and-internal-classes"></a>外部和內部類別

 對於在給定時間使用的每個資料庫 **,sys.bandwidth_usage**視圖返回顯示頻寬使用類和方向的行。 下列範例說明所指資料庫可能會公開的資料。 在這個範例中，時間是 2012-04-21 17:00:00，發生在尖峰時段。 資料庫名稱為 Db1。 在此範例中 **,sys.bandwidth_usage**為入口和出口方向以及外部和內部類的所有四個組合返回了一行,如下所示:  
  
|time|database_name|direction|Class - 類別|time_period|quantity|  
|----------|--------------------|---------------|-----------|------------------|--------------|  
|2012-04-21 17:00:00|Db1|輸入|外部|Peak|66|  
|2012-04-21 17:00:00|Db1|輸出|外部|Peak|741|  
|2012-04-21 17:00:00|Db1|輸入|內部|Peak|1052|  
|2012-04-21 17:00:00|Db1|輸出|內部|Peak|3525|  
  
### <a name="interpreting-data-direction-for-ssgeodr"></a>解譯 [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)] 的資料方向

 如果是 [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)]，頻寬使用量資料會同時在連續複製關聯性兩端的邏輯 master 資料庫中顯示。 因此,您必須從要查詢的資料庫的角度解釋入口和出口方向指示器。 例如，請考慮從來源伺服器傳送 1MB 資料至目標伺服器的複寫資料流。 在這種情況下，1MB 在來源伺服器上會計入傳送的總資料量中，而在目標伺服器上，1MB 會記錄為接收的資料。  
  
> [!NOTE]  
> 傳送的大量資料是依照使用者資料流程的方向，從來源伺服器傳送到目標伺服器。 不過，有些資料需朝其他方向傳送。  
