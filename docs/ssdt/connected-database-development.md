---
title: 連接的資料庫開發
description: 了解 SQL Server Data Tools 搭配連線資料庫的運作方式。 了解如何瀏覽實體、設計資料表、編輯指令碼，以及執行其他工作。
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: 21f7f959-7b8e-4335-8681-bebcd957692c
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 340df9136dd674f4d340779dfc3d2d5e4db32042
ms.sourcegitcommit: b860fe41b873977649dca8c1fd5619f294c37a58
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/29/2020
ms.locfileid: "85519068"
---
# <a name="connected-database-development"></a>連接的資料庫開發

本節將說明 SQL Server Data Tools 所提供用於設計及查詢連接的資料庫的功能。  
  
使用 Visual Studio 的 [SQL Server 物件總管]，開發人員現在可以建立、編輯和瀏覽位於內部部署資料庫伺服器 (例如 SQL Server 2008 或 Microsoft SQL Server 2012) 或外部部署 SQL Azure 中的資料庫物件。 開發人員可以輕易地將現有的生產資料庫複製到測試執行個體，對其執行其開發工作，並將變更發行回生產資料庫。  
  
> [!NOTE]  
> 本節的 HOW TO 主題包含一系列可依序完成的工作。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|說明|  
|---------|---------------|  
|[操作說明：連線到資料庫及瀏覽現有物件](../ssdt/how-to-connect-to-a-database-and-browse-existing-objects.md)|連接到資料庫並瀏覽其實體。|  
|[操作說明：使用資料表設計工具建立資料庫物件](../ssdt/how-to-create-database-objects-using-table-designer.md)|使用新的資料表設計工具，設計資料表及管理資料表關聯性。|  
|[操作說明：使用 Power Buffer 更新連線的資料庫](../ssdt/how-to-update-a-connected-database-with-power-buffer.md)|不必撰寫 ALTER 指令碼，就能更新連接的資料庫。|  
|[篩選與排序對話方塊](../ssdt/filter-and-sort-dialog-box.md)|指定應該在資料檢視中顯示的資料。|  
|[操作說明：使用查詢建立新的資料庫物件](../ssdt/how-to-create-new-database-objects-using-queries.md)|使用 Transact\-SQL 編輯器，編輯及執行 Transact\-SQL 指令碼。|  
|[操作說明：使用查詢編輯現有資料表](../ssdt/how-to-edit-an-existing-table-using-queries.md)|撰寫 Transact\-SQL 指令碼，以編輯資料表定義或填入資料。|  
|[操作說明：檢視及編輯資料表中的資料](../ssdt/how-to-view-and-edit-data-in-a-table.md)|使用資料編輯器，在資料表中檢視或輸入資料。|  
|[操作說明：刪除物件及解析相依性](../ssdt/how-to-delete-objects-and-resolve-dependencies.md)|重新命名或刪除資料庫實體，讓 SQL Server Data Tools 自動解析物件依存性。|  
|[操作說明：複製現有的資料庫](../ssdt/how-to-clone-an-existing-database.md)|從生產資料庫建立開發資料庫。|  
|[擷取、發行及註冊 .dacpac 檔案](../ssdt/extract-publish-and-register-dacpac-files.md)|說明如何擷取及發行 .dacpac 檔案。|  
  
## <a name="related-sections"></a>相關章節

[管理資料表、關聯性及修正錯誤](../ssdt/manage-tables-relationships-and-fix-errors.md)