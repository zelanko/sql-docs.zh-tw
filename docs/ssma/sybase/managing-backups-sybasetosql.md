---
title: 管理 (SybaseToSQL) 的備份 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester Component,Managing Backups
ms.assetid: 266d987c-ecc5-4fa4-bfdf-8c584f1a1332
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 2a7a32804d3c4cb08f593398e901bed66d124b2a
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/07/2020
ms.locfileid: "87931076"
---
# <a name="managing-backups-sybasetosql"></a>管理備份 (SybaseToSQL)
Sybase 備份管理可讓您在執行測試之前或之後備份和還原資料表資料。 您也可以使用 [管理備份內容] 對話方塊來管理 [備份內容]。  
  
## <a name="sybase-backup-management"></a>Sybase 備份管理  
  
### <a name="backup"></a>Backup  
若要開啟 [備份] 對話方塊，請在 [測試者] 功能表上指向 [Sybase 備份管理]，然後按一下 [備份 ...]。在 [備份] 對話方塊中，您會看到 Sybase 中繼資料樹狀結構，其中顯示已載入之 Sybase 架構的所有資料表。 選取一或多個資料表來執行備份。  
  
對話方塊上提供下列按鈕：  
  
-   按一下 [**檢查狀態**] 按鈕，檢查資料表的備份狀態。  
  
-   按一下 [**備份**] 按鈕，備份資料表的資料。  
  
-   按一下 [**取消**] 按鈕以關閉對話方塊。  
  
### <a name="restore"></a>還原  
若要開啟 [還原] 對話方塊，請在 [測試者] 功能表上指向 [Sybase 備份管理]，然後按一下 [還原]。您會在這裡找到一個樹狀結構，其中包含備份中可用的資料表。 選取一或多個資料表來還原其資料。  
  
對話方塊上提供下列按鈕：  
  
-   按一下 [**檢查狀態**] 按鈕，檢查資料表的備份狀態。  
  
-   按一下 [**還原**] 按鈕，將備份資料還原到資料表中。  
  
-   按一下 [**取消**] 按鈕以關閉對話方塊。  
  
### <a name="managing-backup-contents"></a>管理備份內容  
若要開啟 [管理備份內容]，請在 [測試者] 功能表上指向 [Sybase 備份管理]，然後按一下 [備份內容]。您會在這裡找到一個樹狀結構，其中包含備份中的資料表。  
  
對話方塊上提供下列按鈕：  
  
-   按一下 [**檢查狀態**] 按鈕，檢查資料表的備份狀態。  
  
-   按一下 [**移除**] 按鈕，從備份中移除資料表。  
  
-   按一下 [**關閉**] 按鈕以關閉對話方塊。  
  
## <a name="sql-server-backup-management"></a>SQL Server 備份管理  
SQL Server 備份管理可讓您在執行測試之前或之後備份和還原資料表資料。 您也可以使用 [管理備份內容] 對話方塊來管理 [備份內容]。  
  
### <a name="backup"></a>Backup  
若要開啟 [備份] 對話方塊，請在 [測試者] 功能表上指向 [SQL Server 備份管理]，然後按一下 [備份 ...]。 在 [備份] 對話方塊中，您會找到 SQL Server 中繼資料樹狀目錄，其中顯示已載入 SQL Server 資料庫的所有資料表。 選取一或多個資料表來執行備份。  
  
對話方塊上提供下列按鈕：  
  
-   按一下 [**檢查狀態**] 按鈕，檢查資料表的備份狀態。  
  
-   按一下 [**備份**] 按鈕以備份資料表的資料。  
  
-   按一下 [**取消**] 按鈕以關閉對話方塊。  
  
### <a name="restore"></a>還原  
若要開啟 [還原] 對話方塊，請在 [測試者] 功能表上指向 [SQL Server 備份管理]，然後按一下 [還原]。您會在這裡找到一個樹狀結構，其中包含備份中可用的資料表。 請選取一或多個資料表來還原其資料。  
  
對話方塊上提供下列按鈕：  
  
-   按一下 [**檢查狀態**] 按鈕，檢查資料表的備份狀態。  
  
-   按一下 [**還原**] 按鈕，將備份資料還原到資料表中。  
  
-   按一下 [**取消**] 按鈕以關閉對話方塊。  
  
### <a name="managing-backup-contents"></a>管理備份內容  
若要開啟 [管理備份內容]，請在 [測試者] 功能表上指向 [SQL Server 備份管理]，然後按一下 [備份內容]。您會在這裡找到一個樹狀結構，其中包含備份中的資料表。  
  
對話方塊上提供下列按鈕：  
  
-   按一下 [**檢查狀態**] 按鈕，檢查資料表的備份狀態。  
  
-   按一下 [**移除**] 按鈕，從備份中移除資料表。  
  
-   按一下 [**關閉**] 按鈕以關閉對話方塊。  
  
## <a name="see-also"></a>另請參閱  
[&#40;SybaseToSQL&#41;測試遷移的資料庫物件](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
