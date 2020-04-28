---
title: 啟動 sqlcmd 公用程式
ms.custom: seo-lt-2019
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 00d57437-7a29-4da1-b639-ee990db055fb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 80f8f63b4ddb3e8641ef503a615d57c63be35164
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "75243274"
---
# <a name="start-the-sqlcmd-utility"></a>啟動 sqlcmd 公用程式
  若要開始使用 `sqlcmd`，您必須先啟動該公用程式並連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。 您可以連接到預設或具名執行個體。 啟動 `sqlcmd` 公用程式是第一個步驟。  
  
> [!NOTE]  
>  `sqlcmd` 的預設驗證模式為 Windows 驗證。 若要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證，必須使用 **-U** 和 **-P** 選項來指定使用者名稱及密碼。  
  
> [!NOTE]  
>  根據預設， [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 會安裝成具名執行個體 **sqlexpress**。  
  
 如果您從未連接過此 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的執行個體，可能必須設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以接受連接。  
  
### <a name="to-start-the-sqlcmd-utility-and-connect-to-a-default-instance-of-sql-server"></a>啟動 sqlcmd 公用程式和連接 SQL Server 的預設執行個體  
  
1.  在 [**開始**] 功能表上按一下 [**執行**]。 在 [開啟]**** 方塊中，輸入 **cmd**，然後按一下 [確定]**** 開啟 [命令提示字元] 視窗。  
  
2.  在命令提示字元中，輸入 `sqlcmd`。  
  
3.  按 ENTER 鍵。  
  
     現在，您已經有了信任連接，連接了電腦上所執行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的預設執行個體。  
  
     **1>** 是指定`sqlcmd`行號的提示。 每按一次 ENTER 鍵，這個號碼就會增加 1。  
  
4.  若要結束`sqlcmd`會話，請`EXIT`在`sqlcmd`提示字元中輸入。  
  
### <a name="to-start-the-sqlcmd-utility-and-connect-to-a-named-instance-of-sql-server"></a>啟動 sqlcmd 公用程式並連接到 SQL Server 的具名執行個體  
  
1.  開啟 [命令提示字元] 視窗， `sqlcmd -S`然後輸入*myServer\instanceName*。 以要連接的電腦名稱和 *的執行個體來取代* myServer\instanceName [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
2.  按 ENTER 鍵。  
  
     [ `sqlcmd`提示（1>）] 表示您已連接到指定的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]實例。  
  
    > [!NOTE]  
    >  輸入的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式會儲存在緩衝區。 當遇到 GO 命令時，這些陳述式會當做批次來執行。  
  
## <a name="see-also"></a>另請參閱  
 [使用 sqlcmd 執行 Transact-SQL 指令碼檔案](sqlcmd-run-transact-sql-script-files.md)  
  
  
