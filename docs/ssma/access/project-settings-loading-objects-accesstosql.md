---
title: "專案 （載入物件） 的設定 (AccessToSQL) |Microsoft 文件"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 9ec1c1e8-a3e1-4e81-bf49-631f87daa209
caps.latest.revision: 4
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 84737c6b747174f993765a6d86081759cfedd4bb
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="project-settings-loading-objects-accesstosql"></a>專案 （載入物件） 的設定 (AccessToSQL)
載入物件的專案設定可讓您設定如何存取資料庫物件同步處理與 SQL Server 資料庫物件。  
  
從 Access 資料庫重新整理物件以及同步處理與 SQL Server 資料庫的物件指定預設設定的預設動作。 如需詳細資訊，請參閱[從資料庫 &#40; 重新整理AccessToSQL &#41;](../../ssma/access/refresh-from-database-accesstosql.md)  
  
您可以存取兩個不同的同步處理頁面包含相同的設定：  
  
-   設定為所有未來的 SSMA 專案，指定上**工具**功能表上，按一下**DefaultProject 設定**，然後按一下 **載入物件**在左窗格底部。  
  
-   若要指定目前的專案中，設定**工具**功能表上，按一下**專案設定**，然後按一下 **載入物件**在左窗格底部。  
  
## <a name="options"></a>選項  
  
##### <a name="misc"></a>其他  
  
##### <a name="attempts"></a>嘗試  
提供物件採取載入 SQL Server 的行程數目的相關資訊。 載入 SQL Server 中的物件通常是在多個階段中執行。 無法載入在第一個階段中，例如外部索引鍵的物件可能已成功載入下個階段。  
  
根據預設值為 2。  
  
## <a name="synchronization-for-sql-server"></a>SQL Server 的同步處理  
  
##### <a name="default-action-on-local-and-remote-object-change"></a>本機和遠端物件變更時的預設動作  
物件定義變更 SSMA 和資料庫伺服器時，同步處理 對話方塊中指定的預設設定。  
  
-   如果您選取**從資料庫重新整理**，SSMA 會將載入資料庫定義的中繼資料時即符合此條件。  
  
-   如果您選取**寫入資料庫**，SSMA 滿足條件時，會更新根據 SSMA 中繼資料內容，在資料庫中的物件。  
  
-   如果您選取**略過**，SSMA 將不會執行重新整理的任何動作。  
  
##### <a name="default-action-on-local-object-change"></a>在本機的物件變更的預設動作  
SSMA 物件發生變更時，同步處理 對話方塊中指定的預設設定。  
  
-   如果您選取**從資料庫重新整理**，SSMA 會將載入資料庫定義的中繼資料時即符合此條件。  
  
-   如果您選取**寫入資料庫**，SSMA 滿足條件時，會更新根據 SSMA 中繼資料內容，在資料庫中的物件。  
  
-   如果您選取**略過**，SSMA 將不會執行重新整理的任何動作。  
  
##### <a name="default-action-on-remote-object-change"></a>變更遠端物件的預設動作  
當資料庫伺服器上變更物件時，同步處理 對話方塊中指定的預設設定。  
  
-   如果您選取**從資料庫重新整理**，SSMA 會將載入資料庫定義的中繼資料時即符合此條件。  
  
-   如果您選取**寫入資料庫**，SSMA 滿足條件時，會更新根據 SSMA 中繼資料內容，在資料庫中的物件。  
  
-   如果您選取**略過**，SSMA 將不會執行重新整理的任何動作。  
  
##### <a name="default-action-when-local-object-metadata-is-missing"></a>遺漏本機物件中繼資料時的預設動作  
遺漏本機中繼資料時，同步處理 對話方塊中指定的預設設定。  
  
-   如果您選取**從資料庫重新整理**，SSMA 重新整理會從選取資料庫 選項時即符合此條件。  
  
-   如果您選取**寫入資料庫**，SSMA 將物件從資料庫中刪除時即符合此條件。  
  
-   如果您選取**略過**，SSMA 將不會執行重新整理的任何動作。  
  

