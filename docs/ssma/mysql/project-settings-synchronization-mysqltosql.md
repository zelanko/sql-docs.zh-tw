---
title: "專案設定 （同步處理） (MySQLToSQL) |Microsoft 文件"
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
ms.assetid: 42061ff7-e6e7-497b-a0d9-440b9cf5986c
caps.latest.revision: 3
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2b2fcc99f40b7d06cdb9bb831cee5b5bf7490f7e
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="project-settings-synchronization-mysqltosql"></a>專案設定 （同步處理） (MySQLToSQL)
同步處理**專案設定**可讓您設定 MySQL 資料庫物件如何同步處理與 SQL Server 資料庫物件。  
  
從 MySQL 資料庫重新整理物件以及同步處理與 SQL Server 資料庫的物件指定預設設定的預設動作。 如需詳細資訊，請參閱[從資料庫 &#40; 重新整理MySQLToSQL &#41;](../../ssma/mysql/refresh-from-database-mysqltosql.md)  
  
您可以存取兩個不同的同步處理頁面包含相同的設定：  
  
-   設定為所有未來的 SSMA 專案，指定上**工具**功能表上，按一下**DefaultProject 設定**，然後按一下 **同步處理**在左窗格底部。  
  
-   若要指定目前的專案中，設定**工具**功能表上，按一下**專案設定**，然後按一下 **同步處理**在左窗格底部。  
  
## <a name="options"></a>選項。  
  
##### <a name="misc"></a>其他  
  
##### <a name="attempts"></a>嘗試  
提供物件採取載入 SQL Server 的行程數目的相關資訊。 載入 SQL Server 中的物件通常是在多個階段中執行。 無法載入在第一個階段中，例如外部索引鍵的物件可能已成功載入下個階段。  
  
根據預設值為 2。  
  
## <a name="synchronization-for-mysql"></a>用於 MySQL 的同步處理  
  
##### <a name="action-on-local-and-remote-object-change"></a>本機和遠端物件變更時採取的動作  
物件定義變更 SSMA 和資料庫伺服器時，同步處理 對話方塊中指定的預設設定。  
  
-   如果您從資料庫選取重新整理，SSMA 會將載入資料庫定義的中繼資料時即符合此條件。  
  
-   如果您選取 略過，SSMA 不會執行重新整理的任何動作。  
  
##### <a name="action-on-local-object-change"></a>本機物件變更時採取的動作  
SSMA 物件發生變更時，同步處理 對話方塊中指定的預設設定。  
  
-   如果您選取**從資料庫重新整理**，SSMA 會將載入資料庫定義的中繼資料時即符合此條件。  
  
-   如果您選取**略過**，SSMA 將不會執行重新整理的任何動作。  
  
##### <a name="action-on-remote-object-change"></a>遠端物件變更時採取的動作  
當資料庫伺服器上變更物件時，同步處理 對話方塊中指定的預設設定。  
  
-   如果您選取**從資料庫重新整理**，SSMA 會將載入資料庫定義的中繼資料時即符合此條件。  
  
-   如果您選取**略過**，SSMA 將不會執行重新整理的任何動作。  
  
##### <a name="action-when-local-object-metadata-is-missing"></a>遺漏本機物件的中繼資料時的動作  
遺漏本機中繼資料時，同步處理 對話方塊中指定的預設設定。  
  
-   如果您選取**從資料庫重新整理**，SSMA SSMA 會將載入資料庫定義的中繼資料時即符合此條件。  
  
-   如果您選取**略過**，SSMA 將不會執行任何重新整理的動作  
  
## <a name="synchronization-for-sql-server"></a>SQL Server 的同步處理  
  
##### <a name="action-on-local-and-remote-object-change"></a>本機和遠端物件變更時採取的動作  
物件定義變更 SSMA 和資料庫伺服器時，同步處理 對話方塊中指定的預設設定。  
  
-   如果您選取**從資料庫重新整理**，SSMA 會將載入資料庫定義的中繼資料時即符合此條件。  
  
-   如果您選取**寫入資料庫**，SSMA 滿足條件時，會更新根據 SSMA 中繼資料內容，在資料庫中的物件。  
  
-   如果您選取**略過**，SSMA 將不會執行重新整理的任何動作。  
  
##### <a name="action-on-local-object-change"></a>本機物件變更時採取的動作  
SSMA 物件發生變更時，同步處理 對話方塊中指定的預設設定。  
  
-   如果您選取**從資料庫重新整理**，SSMA 會將載入資料庫定義的中繼資料時即符合此條件。  
  
-   如果您選取**寫入資料庫**，SSMA 滿足條件時，會更新根據 SSMA 中繼資料內容，在資料庫中的物件。  
  
-   如果您選取**略過**，SSMA 將不會執行重新整理的任何動作。  
  
##### <a name="action-on-remote-object-change"></a>遠端物件變更時採取的動作  
當資料庫伺服器上變更物件時，同步處理 對話方塊中指定的預設設定。  
  
-   如果您選取**從資料庫重新整理**，SSMA 會將載入資料庫定義的中繼資料時即符合此條件。  
  
-   如果您選取**寫入資料庫**，SSMA 滿足條件時，會更新根據 SSMA 中繼資料內容，在資料庫中的物件。  
  
-   如果您選取**略過**，SSMA 將不會執行重新整理的任何動作。  
  
##### <a name="action-when-local-object-metadata-is-missing"></a>遺漏本機物件的中繼資料時的動作  
遺漏本機中繼資料時，同步處理 對話方塊中指定的預設設定。  
  
-   如果您選取**從資料庫重新整理**，SSMA 重新整理會從選取資料庫 選項時即符合此條件。  
  
-   如果您選取**寫入資料庫**，SSMA 將物件從資料庫中刪除時即符合此條件。  
  
-   如果您選取**略過**，SSMA 將不會執行重新整理的任何動作。  
  

