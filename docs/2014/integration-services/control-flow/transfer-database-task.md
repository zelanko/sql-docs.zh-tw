---
title: 傳送資料庫工作 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferdatabasetask.f1
helpviewer_keywords:
- Transfer Database task [Integration Services]
ms.assetid: b9a2e460-cdbc-458f-8df8-06b8b2de3d67
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f7ddf838269932c19b0614d5a5219a7f03daed17
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62830147"
---
# <a name="transfer-database-task"></a>傳送資料庫工作
  「傳送資料庫」工作會在兩個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體之間傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫。 與其他只能透過複製 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件來傳送它們的工作不同，「傳送資料庫」工作可以複製或移動資料庫。 這項工作也可用來在同一部伺服器內複製資料庫。  
  
## <a name="offline-and-online-modes"></a>離線和線上模式  
 資料庫可以使用線上或離線模式傳送。 當您使用線上模式時，資料庫會保持附加狀態，並使用 SQL Management Object (SMO) 複製資料庫物件來進行傳送。 當您使用離線模式時，會卸離資料庫，複製或移動資料庫檔案，並在傳送成功完成後將資料庫附加至目的地。 如果複製資料庫，則會在成功複製後將資料庫自動重新附加至來源。 在離線模式中，資料庫的複製速度會更快，但使用者在傳送期間無法使用資料庫。  
  
 離線模式需要您在包含資料庫檔案的來源和目的地伺服器上，指定網路檔案共用。 如果資料夾已共用，且可由使用者存取，則您可以使用語法 \\\computername\Program Files\myfolder\\參考網路共用。 否則，您必須使用語法 \\\computername\c$\Program Files\myfolder\\。 若要使用後面的語法，使用者必須具有來源和目的地網路共用的寫入權限。  
  
## <a name="transfer-of-databases-between-versions-of-sql-server"></a>在 SQL Server 的版本之間傳送資料庫  
 「傳送資料庫」工作可以在不同 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本的執行個體之間，傳送資料庫。  
  
## <a name="events"></a>事件  
 「傳送資料庫」工作並不報告錯誤訊息傳送的累加進度，它只報告 0% 和 100 % 完成。  
  
## <a name="execution-value"></a>執行值  
 執行值 (在工作的 `ExecutionValue` 屬性中定義) 會傳回值 1，因為與其他傳送工作不同，「傳送資料庫」工作只能傳送一個資料庫。  
  
 透過將使用者自訂變數指派給「傳送資料庫」工作的 `ExecValueVariable` 屬性，可將與錯誤訊息傳送相關的資訊用於封裝中的其他物件。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](../integration-services-ssis-variables.md)和[在封裝中使用變數](../use-variables-in-packages.md)。  
  
## <a name="log-entries"></a>記錄項目  
 「傳送資料庫」工作包含下列自訂記錄項目：  
  
-   SourceSQLServer    此記錄項目列出來源伺服器的名稱。  
  
-   DestSQLServer    此記錄項目列出目的地伺服器的名稱。  
  
-   SourceDB    此記錄項目列出傳送之資料庫的名稱。  
  
 另外，在覆寫目的地資料庫時，會寫入 `OnInformation` 事件的記錄項目。  
  
## <a name="security-and-permissions"></a>安全性和權限  
 若要使用離線模式傳送資料庫，執行封裝的使用者必須是 sysadmin 伺服器角色的成員。  
  
 若要使用線上模式傳送資料庫，執行封裝的使用者必須是 sysadmin 伺服器角色的成員，或是選取之資料庫的資料庫擁有者 (dbo)。  
  
## <a name="configuration-of-the-transfer-database-task"></a>傳送資料庫工作的組態  
 您可以指定如果資料庫傳送失敗，工作是否嘗試重新附加來源資料庫。  
  
 「傳送資料庫」工作還可設為允許覆寫具有相同名稱的目的地資料庫，以取代目的地資料庫。  
  
 來源資料庫還可以重新命名為傳送處理序的一部分。 如果您想要將資料庫傳送至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的目的地執行個體，而該執行個體已包含相同名稱的資料庫，則重新命名來源資料庫便可允許傳送資料庫。 不過，資料庫檔案名稱也必須不同，如果目的地上已存在具有相同名稱的資料庫檔案，則工作會失敗。  
  
 當您複製資料庫時，資料庫不能小於目的地伺服器上的 **model** 資料庫大小。 您可以增加要複製的資料庫大小，或減少 **model**的大小。  
  
 在執行階段，「傳送資料庫」工作會使用一或兩個 SMO 連接管理員，連接到來源和目的地伺服器。 當您在同一伺服器上建立資料庫的副本時，只需要一個 SMO 連接管理員。 SMO 連接管理員會在「傳送資料庫」工作以外另行設定，然後在「傳送資料庫」工作中參考。 當工作存取伺服器時，SMO 連接管理員會指定要使用的伺服器和驗證模式。 如需詳細資訊，請參閱 [SMO Connection Manager](../connection-manager/smo-connection-manager.md)。  
  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需有關可以在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [傳送資料庫工作編輯器 &#40;一般頁面&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [傳送資料庫工作編輯器 &#40;資料庫頁面&#41;](../transfer-database-task-editor-databases-page.md)  
  
-   [運算式頁面](../expressions/expressions-page.md)  
  
 如需有關如何在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定這些屬性的詳細資訊，請按下列主題：  
  
-   [設定工作或容器的屬性](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-transfer-database-task"></a>傳送資料庫工作的程式設計組態  
 如需有關以程式設計方式設定這些屬性的詳細資訊，請按下列主題：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferDatabaseTask.TransferDatabaseTask>  
  
  
