---
title: 連線到 Oracle 來源資料庫 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- oraDb
ms.assetid: 220cf555-0db2-443c-8f87-8e413f3ca731
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 565f88565a797c2f902b2df4f42deea631b34bb4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48114218"
---
# <a name="connect-to-an-oracle-source-database"></a>連接到 Oracle 來源資料庫
  使用 [Oracle 來源] 頁面可提供連接至 Oracle 來源資料庫所需的資訊。 此 CDC 執行個體將會讀取您所連接之 Oracle 資料庫的重做記錄。  
  
 **Oracle 連接字串**  
 輸入電腦與您使用之 Oracle 資料庫之間的 Oracle 連接字串。 連接字串會以下列其中一種方式撰寫：  
  
 `host[:port][/service name]`  
  
 連接字串還可以指定 Oracle Net 連接描述項，例如， `(DESCRIPTION=(ADDRESS=(PROTOCOL=tcp) (HOST=erp.contoso.com) (PORT=1521)) (CONNECT_DATA=(SERVICE_NAME=orcl)))`  
  
 如果使用目錄伺服器或 tnsnames，則連接字串可以是連接的名稱。  
  
 **Oracle 記錄採礦驗證**  
 若要輸入已被授權進行記錄採礦之 Oracle 資料庫使用者的認證，請選取下列其中一項：  
  
-   **Windows 驗證**：選取此選項可使用目前的 Windows 網域認證。 只有當設定 Oracle 資料庫使用 Windows 驗證時，才可使用這個選項。  
  
-   **Oracle 驗證**：如果您選取這個選項，您必須在您所連接的 Oracle 資料庫中輸入使用者的 **[使用者名稱]** 和 **[密碼]** 。  
  
> [!NOTE]  
>  使用者必須擁有 Oracle 資料庫中授與的以下權限，才能成為記錄採礦使用者。  
>   
>  -   SELECT on \<任何擷取的資料表>  
> -   SELECT ANY TRANSACTION  
> -   EXECUTE on DBMS LOGMNR  
> -   SELECT on V$LOGMNR CONTENTS  
> -   SELECT on V$ARCHIVED LOG  
> -   SELECT on V$LOG  
> -   SELECT on V$LOGFILE  
> -   SELECT on V$DATABASE  
> -   SELECT on V$THREAD  
> -   SELECT on ALL INDEXES  
> -   SELECT on ALL OBJECTS  
> -   SELECT on DBA OBJECTS  
> -   SELECT on ALL TABLES  
>   
>  如果有任何權限不能授與給 V$xxx，則將該權限授與給 V_S$xxx。  
  
 **測試連接**  
 按一下 [測試連接]，以判斷您是否已經與擁有 Oracle 資料庫的遠端電腦建立連接。 隨即開啟對話方塊，通知您連接是否成功。  
  
> [!IMPORTANT]  
>  由於已知問題的緣故，如果未以系統管理員的身分執行 CDC 設計工具，則 Oracle 來源資料庫的連接可能會失敗。 如果連接失敗，請使用 **[以系統管理員身分執行]** 選項關閉 CDC 設計工具，然後重新啟動。  
  
 當您在這個頁面上輸入資訊完畢後，請按 **[下一步]** [Select Oracle Tables and Columns](select-oracle-tables-and-columns.md)。  
  
## <a name="see-also"></a>另請參閱  
 [如何建立 SQL Server 變更資料庫執行個體](how-to-create-the-sql-server-change-database-instance.md)   
 [編輯執行個體屬性](edit-instance-properties.md)  
  
  
