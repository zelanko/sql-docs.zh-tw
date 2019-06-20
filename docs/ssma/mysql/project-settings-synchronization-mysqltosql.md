---
title: 專案設定 （同步處理） (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 42061ff7-e6e7-497b-a0d9-440b9cf5986c
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: e82fa9d02fdbfe876f4097c54c6877c3a3a81fee
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62473904"
---
# <a name="project-settings-synchronization-mysqltosql"></a>專案設定 (同步處理) (MySQLToSQL)
同步處理**專案設定**可讓您設定 MySQL 資料庫物件如何同步處理使用 SQL Server 資料庫物件。  
  
重新整理從 MySQL 資料庫的物件，並與 SQL Server 資料庫同步處理物件的預設動作會指定預設設定。 如需詳細資訊，請參閱 <<c0> [ 從資料庫重新整理&#40;MySQLToSQL&#41;</c0>](../../ssma/mysql/refresh-from-database-mysqltosql.md)  
  
您可以存取兩個不同的同步處理頁面，其中包含相同的設定：  
  
-   上指定的所有未來的 SSMA 專案，設定**工具**功能表上，按一下**DefaultProject 設定**，然後按一下**同步處理**左窗格的底部。  
  
-   若要指定目前的專案中，設定**工具** 功能表中，按一下**專案設定**，然後按一下**同步處理**左窗格的底部。  
  
## <a name="options"></a>選項。  
  
##### <a name="misc"></a>其他  
  
##### <a name="attempts"></a>嘗試  
提供物件載入 SQL Server 要花多少個階段的資訊。 載入 SQL Server 中的物件通常是在多個階段中執行。 在下一個階段中，可能會成功地載入無法在第一個階段中，例如外部索引鍵，載入的物件。  
  
根據預設值為 2。  
  
## <a name="synchronization-for-mysql"></a>適用於 MySQL 的同步處理  
  
##### <a name="action-on-local-and-remote-object-change"></a>本機和遠端物件變更時採取的動作  
SSMA 中和資料庫伺服器上，對物件定義變更時，請在同步處理 對話方塊中指定的預設設定。  
  
-   如果您從資料庫選取 重新整理，SSMA 會將載入資料庫定義的中繼資料時即符合此條件。  
  
-   如果您選取 略過，SSMA 不會執行重新整理的任何動作。  
  
##### <a name="action-on-local-object-change"></a>本機物件變更時採取的動作  
SSMA 中的物件變更時，請在同步處理 對話方塊中指定的預設設定。  
  
-   如果您選取**從資料庫重新整理**，SSMA 會將載入資料庫定義的中繼資料時即符合此條件。  
  
-   如果您選取**略過**，SSMA 將不會執行重新整理的任何動作。  
  
##### <a name="action-on-remote-object-change"></a>遠端物件變更時採取的動作  
資料庫伺服器上的物件變更時，請在同步處理 對話方塊中指定的預設設定。  
  
-   如果您選取**從資料庫重新整理**，SSMA 會將載入資料庫定義的中繼資料時即符合此條件。  
  
-   如果您選取**略過**，SSMA 將不會執行重新整理的任何動作。  
  
##### <a name="action-when-local-object-metadata-is-missing"></a>遺漏本機物件的中繼資料時的動作  
遺漏本機中繼資料時，請在同步處理 對話方塊中指定的預設設定。  
  
-   如果您選取**從資料庫重新整理**，SSMA 會將載入資料庫定義的中繼資料時即符合此條件。  
  
-   如果您選取**略過**，SSMA 將不會執行任何重新整理動作  
  
## <a name="synchronization-for-sql-server"></a>適用於 SQL Server 的同步處理  
  
##### <a name="action-on-local-and-remote-object-change"></a>本機和遠端物件變更時採取的動作  
SSMA 中和資料庫伺服器上，對物件定義變更時，請在同步處理 對話方塊中指定的預設設定。  
  
-   如果您選取**從資料庫重新整理**，SSMA 會將載入資料庫定義的中繼資料時即符合此條件。  
  
-   如果您選取**寫入資料庫**，SSMA 在符合條件時，會更新根據 SSMA 中繼資料內容，在資料庫中的物件。  
  
-   如果您選取**略過**，SSMA 將不會執行重新整理的任何動作。  
  
##### <a name="action-on-local-object-change"></a>本機物件變更時採取的動作  
SSMA 中的物件變更時，請在同步處理 對話方塊中指定的預設設定。  
  
-   如果您選取**從資料庫重新整理**，SSMA 會將載入資料庫定義的中繼資料時即符合此條件。  
  
-   如果您選取**寫入資料庫**，SSMA 在符合條件時，會更新根據 SSMA 中繼資料內容，在資料庫中的物件。  
  
-   如果您選取**略過**，SSMA 將不會執行重新整理的任何動作。  
  
##### <a name="action-on-remote-object-change"></a>遠端物件變更時採取的動作  
資料庫伺服器上的物件變更時，請在同步處理 對話方塊中指定的預設設定。  
  
-   如果您選取**從資料庫重新整理**，SSMA 會將載入資料庫定義的中繼資料時即符合此條件。  
  
-   如果您選取**寫入資料庫**，SSMA 在符合條件時，會更新根據 SSMA 中繼資料內容，在資料庫中的物件。  
  
-   如果您選取**略過**，SSMA 將不會執行重新整理的任何動作。  
  
##### <a name="action-when-local-object-metadata-is-missing"></a>遺漏本機物件的中繼資料時的動作  
遺漏本機中繼資料時，請在同步處理 對話方塊中指定的預設設定。  
  
-   如果您選取**從資料庫重新整理**，SSMA 會選取從 [資料庫] 選項重新整理時即符合此條件。  
  
-   如果您選取**寫入資料庫**，SSMA 將物件從資料庫刪除時即符合此條件。  
  
-   如果您選取**略過**，SSMA 將不會執行重新整理的任何動作。  
  
