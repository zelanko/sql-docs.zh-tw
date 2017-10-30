---
title: "建立資料表 SQL 陳述式 （SQL Server 匯入和匯出精靈） |Microsoft 文件"
ms.custom: 
ms.date: 02/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.createtablesql.f1
ms.assetid: 0d6f6b3b-d023-4770-a8a9-65b2977c8d05
caps.latest.revision: 67
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ad9b68e2a0ac4cd88917a7b45c7a8f12b14f3ab4
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="create-table-sql-statement-sql-server-import-and-export-wizard"></a>建立資料表的 SQL 陳述式 (SQL Server 匯入和匯出精靈)
如果您選取 [建立目的地資料表]  ，然後在 [資料行對應]  對話方塊中選取 [編輯 SQL]  ，[ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈] 會顯示 [建立資料表的 SQL 陳述式]  對話方塊。 在此頁面上，您可以檢閱並選擇性地自訂 **CREATE TABLE** 命令，精靈將會執行此命令來建立新的目的地資料表。
  
> [!NOTE]
> 如果您想要尋找 [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE TABLE 陳述式的相關資訊，而不是 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈] 之 [建立資料表的 SQL 陳述式] 對話方塊的相關資訊，請參閱 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)。 
  
## <a name="screen-shot-of-the-create-table-sql-statement-page"></a>[建立資料表的 SQL 陳述式] 頁面的螢幕擷取畫面  
 下列螢幕擷取畫面顯示精靈的 [建立資料表的 SQL 陳述式]  對話方塊。
 
在此範例中，[SQL 陳述式]  方塊會包含精靈所產生的預設 **CREATE TABLE** 陳述式。 此陳述式會建立新的目的地資料表，名為**Person.AddressNew** ，是一份**Person.Address**來源資料表。 
  
 ![匯入和匯出精靈建立資料表頁面](../../integration-services/import-export-data/media/create-table.png "匯入和匯出精靈建立資料表頁面")  
  
## <a name="review-or-regenerate-the-create-table-statement"></a>檢視或重新產生 CREATE TABLE 陳述式  
 **SQL 陳述式**  
顯示自動產生的 SQL 陳述式並讓您進行自訂。
 
如果您變更這個預設 CREATE TABLE 命令，您也可能對相關聯的資料行對應進行變更，當您返回**資料行對應** 對話方塊。  
  
若要在 SQL 陳述式的文字中包含歸位字元，請按 CTRL+ENTER 鍵。 如果只按 ENTER 鍵，對話方塊就會關閉。  
  
如需 CREATE TABLE 陳述式和語法的詳細資訊，請參閱 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)。   
  
 **自動產生**  
 如果您已經變更，按一下 還原預設的 SQL 陳述式，**自動產生**。  
  
## <a name="create-a-table-that-includes-a-filestream-column"></a>建立包含 FILESTREAM 資料行的資料表  
 [ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈] 會根據連接的資料來源來產生預設 CREATE TABLE 陳述式。 這個預設 CREATE TABLE 陳述式不會包含 FILESTREAM 屬性，即使來源資料表具有 FILESTREAM 資料行亦然。
 1.  若要使用精靈來複製 FILESTREAM 資料行，請先在目的地資料庫上實作 FILESTREAM 儲存體。
 2.  然後在 [建立資料表的 SQL 陳述式]  對話方塊中，將 FILESTREAM 屬性手動加入 CREATE TABLE 陳述式。  

如需語法的詳細資訊，請參閱[CREATE TABLE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-table-transact-sql.md). 如需 FILESTREAM 的詳細資訊，請參閱[二進位大型物件 &#40;Blob&#41; 資料 &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)。  
  
## <a name="whats-next"></a>下一步  
 檢閱並自訂 CREATE TABLE 命令，然後按一下 [確定] 之後，[建立資料表的 SQL 陳述式]  對話方塊會將您返回 [資料行對應]  對話方塊。 如需詳細資訊，請參閱 [資料行對應](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)。
 
 ## <a name="see-also"></a>另請參閱
[透過匯入和匯出精靈的簡單範例開始使用](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)



