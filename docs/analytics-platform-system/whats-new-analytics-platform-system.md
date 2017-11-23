---
title: "Analytics Platform System-向外延展資料倉儲中最新消息"
author: happynicolle
ms.author: nicw;barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "請參閱什麼是 Microsoft® Analytics Platform System 的新功能，向外延展內部部署裝載 MPP SQL Server 平行資料倉儲應用裝置。"
ms.date: 11/28/2016
ms.topic: article
ms.openlocfilehash: 3dc1a338ced5aa90ada112b97c4a6f13777da409
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="whats-new-in-analytics-platform-system-2016-a-scale-out-mpp-data-warehouse"></a>分析平台系統 2016，向外延展 MPP 資料倉儲中最新消息
請參閱什麼是新的 Microsoft® 分析平台 System (APS) 2016年，向外延展的最新的應用裝置更新內部部署裝載 MPP SQL Server 平行資料倉儲應用裝置。 

## <a name="sql-server-2016"></a>SQL Server 2016

APS 2016 最新的 SQL Server 2016 版本上執行，並使用預設的資料庫相容性等級 130。  SQL Server 2016 可讓您能夠支援某些新的功能，例如次要索引的叢集資料行存放區索引和 Kerberos polybase。 


## <a name="t-sql"></a>T-SQL
APS 2016 支援這些 T-SQL 的相容性增強功能。  這些額外的語言項目讓您更容易從 SQL Server 和其他資料來源移轉。 

- [資料行層級 SQL 定序][]現已支援除了 Windows 定序。
- [在叢集資料行存放區索引上的非叢集索引][]改善搜尋叢集資料行存放區索引中的特定值的查詢效能。 
- [選取此項目...到][] 
- [sp_spaceused()][]顯示使用的磁碟空間，或在資料表或資料庫中保留。
- [寬型資料表][]支援等同於 SQL Server 2016。 32k，資料列大小的前一個限制不存在。 

### <a name="data-types"></a>資料類型

- [Varchar （max)][]， [nvarchar （max)][]和[varbinary （max)][]。 這些 LOB 資料型別有大小上限為 2 GB。 這些載入物件使用[bcp 公用程式][]。 Polybase 和 dwloader 目前不支援這些資料類型。 
- [SYSNAME][]
- [UNIQUEIDENTIFIER][]
- [數值][]和十進位資料類型。

### <a name="window-functions"></a>視窗函數

- [ROWS 或 RANGE][] OVER 子句的 SELECT 陳述式中。
- [FIRST_VALUE][]
- [LAST_VALUE][]
- [CUME_DIST][]
- [PERCENT_RANK][]

### <a name="security-functions"></a>安全性函數

- [CHECKSUM()][]和[BINARY_CHECKSUM()][]
- [HAS_PERMS_BY_NAME()][]

### <a name="additional-functions"></a>其他函式

- [NEWID （)][]
- [RAND （)][]

## <a name="polybasehadoop-enhancements"></a>PolyBase/Hadoop 增強功能

- 2.4 的 Hortonworks HDP 與 HDP 2.5 相容性
- 透過資料庫範圍認證的 Kerberos 支援
- 使用 Azure 儲存體 Blob 的認證支援

## <a name="install-and-upgrade-enhancements"></a>安裝和升級的增強功能

### <a name="enterprise-architecture-updates"></a>企業架構更新
將您現有的應用裝置升級至 AP 2016 安裝的最新的韌體和驅動程式更新，包括安全性修正程式。 

新的裝置從 HPE 或 DELL 包含所有最新的更新加上：

- 最新的層代處理器支援 (Broadwell)
- 更新至 DDR4 dimm 也可能
- 提升的 DIMM 產能

### <a name="integration"></a>整合

- 完整網域名稱 (FQDN) 支援讓您能夠設定至應用裝置的網域信任。 
- 若要使用 FQDN，您需要執行完整的升級，並選擇在升級期間。 

### <a name="reduced-downtime"></a>縮短停機時間
安裝或升級至 AP 2016 速度較快，而且需要較少的停機時間比先前的版本。 若要減少停機時間、 安裝或升級： 

 - 簡化使用包含到 2016 年 6 月的所有更新的映像套用 WSUS 更新
 - 套用安全性更新的驅動程式和韌體更新
 - 應用裝置上將最新的 hotfix 以及應用裝置驗證公用程式 (PAV)，因此，他們就可以不需要進行下載與安裝。


<!--MSDN references-->
[database compatibility level 130]:https://msdn.microsoft.com/library/bb510680.aspx
[資料行層級 SQL 定序]:https://msdn.microsoft.com/library/ms143726.aspx
[在叢集資料行存放區索引上的非叢集索引]:https://msdn.microsoft.com/library/ms188783.aspx
[Varchar （max)]:https://msdn.microsoft.com/library/ms176089.aspx
[nvarchar （max)]:https://msdn.microsoft.com/library/ms186939.aspx
[varbinary （max)]:https://msdn.microsoft.com/library/ms188362.aspx
[SYSNAME]:https://msdn.microsoft.com/library/ms188021.aspx
[選取此項目...到]:https://msdn.microsoft.com/library/ms188029.aspx
[sp_spaceused()]:https://msdn.microsoft.com/library/ms188776.aspx
[寬型資料表]:https://msdn.microsoft.com/library/ms143432.aspx
[BULK INSERT]:https://msdn.microsoft.com/library/ms188365.aspx
[bcp 公用程式]:https://msdn.microsoft.com/library/ms162802.aspx
[UNIQUEIDENTIFIER]:https://msdn.microsoft.com/library/ms187942.aspx
[數值]:https://msdn.microsoft.com/library/ms187746.aspx
[ROWS 或 RANGE]:https://msdn.microsoft.com/library/ms189461.aspx
[FIRST_VALUE]:https://msdn.microsoft.com/library/hh213018.aspx
[LAST_VALUE]:https://msdn.microsoft.com/library/hh231517.aspx
[CUME_DIST]:https://msdn.microsoft.com//library/hh231078.aspx
[PERCENT_RANK]:https://msdn.microsoft.com/library/hh213573.aspx
[CHECKSUM()]:https://msdn.microsoft.com/library/ms189788.aspx
[BINARY_CHECKSUM()]:https://msdn.microsoft.com/library/ms173784.aspx
[HAS_PERMS_BY_NAME()]:https://msdn.microsoft.com/library/ms189802.aspx
[NEWID （)]:https://msdn.microsoft.com/library/ms190348.aspx
[RAND （)]:https://msdn.microsoft.com/library/ms177610.aspx


  

  


