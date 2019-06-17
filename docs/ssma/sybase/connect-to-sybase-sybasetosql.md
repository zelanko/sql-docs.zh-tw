---
title: 連接到 Sybase (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 524f95ef-10bd-497c-84ca-c06a0ae794fb
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 0805246d5b88138cfa97019d1e0cd524c82456c6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63061001"
---
# <a name="connect-to-sybase-sybasetosql"></a>連線到 Sybase (SybaseToSQL)
使用**連接到 Sybase**對話方塊連接到您想要移轉的 Sybase Adaptive Server Enterprise (ASE) 執行個體。  
  
若要存取此對話方塊中，在**檔案**功能表上，選取**連接到 Sybase**。 如果您先前曾經連線，則命令是**重新連接到 Sybase**。  
  
## <a name="options"></a>選項。  
**提供者**  
選取任何連接到 Sybase 伺服器電腦上安裝的提供者。  
  
**模式**  
選取其中一個標準或進階的連接模式。 在標準模式中，您可以輸入或選取的伺服器名稱、 連接埠、 使用者名稱和密碼值。 在進階模式中，您可以提供連接字串。  
  
**伺服器名稱**  
輸入或選取的名稱或 IP 位址的自動調整的伺服器。 預設伺服器名稱是電腦名稱相同。 這是標準模式的選項。  
  
**伺服器通訊埠**  
如果您使用非預設連接埠連接到 ASE，請輸入連接埠號碼。 預設連接埠號碼為 5000。 這是標準模式的選項。  
  
**使用者名稱**  
輸入用來連接到 ASE 的使用者名稱。 這是標準模式的選項。  
  
**密碼**  
請輸入使用者名稱的密碼。 這是標準模式的選項。  
  
**連接字串**  
輸入 ASE 的完整連接字串連接。  
  
連接字串是由參數名稱和值配對所組成。 參數的名稱會隨所使用的提供者。  
  
**各種提供者的連接參數如下所示：**  
  
1.  連線參數**OLE DB 提供者**  
  
    |設定|Sybase 12.5 參數|Sybase 15 參數|  
    |-----------|-------------------------|-----------------------|  
    |伺服器名稱|伺服器名稱|[伺服器]|  
    |通訊埠|伺服器連接埠位址|通訊埠|  
    |[使用者名稱]|使用者識別碼|使用者識別碼|  
    |[密碼]|[密碼]|[密碼]|  
    |提供者|提供者|提供者|  
  
    Sybase ASE 12.5，為連接字串範例如下所示：  
  
    `Server Name=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=Sybase.ASEOLEDBProvider;`  
  
    適用於 Sybase ASE 15，連接字串範例如下所示：  
  
    `Server=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=ASEOLEDB;Port=5000;`  
  
2.  連線參數**ODBC 提供者**  
  
    |設定|Sybase 12.5/15 參數|  
    |-----------|-----------------------------|  
    |驅動程式名稱|驅動程式|  
    |伺服器名稱|[伺服器]|  
    |使用者名稱|uid|  
    |[密碼]|pwd|  
    |通訊埠編號|通訊埠|  
  
    Sybase ASE 12.5 或 15，連接字串範例如下所示：  
  
    `driver=Adaptive Server Enterprise;Server=sybserver;uid=MyUserID;pwd=MyP@$$word;Port=5000;`  
  
3.  連線參數**ADO.NET 提供者**  
  
    |設定|Sybase 12.5/15 參數|  
    |-----------|-----------------------------|  
    |伺服器名稱|[伺服器]|  
    |使用者名稱|uid|  
    |[密碼]|pwd|  
    |通訊埠編號|通訊埠|  
  
    下列是 ADO.NET 提供者的連接字串的範例：  
  
    `Server=sybserver;Port=5000;uid=MyUserID;pwd=MyP@$$word;`  
  
如需詳細資訊，請參閱 ASE 文件。  
  
這是進階的模式選項。  
  
