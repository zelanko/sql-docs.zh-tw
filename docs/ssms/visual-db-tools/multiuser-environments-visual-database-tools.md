---
title: 多使用者環境 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- users [SQL Server], multiuser environments
- conflict resolution [Visual Database Tools]
- multiple users making database changes
- multiuser environments [Visual Database Tools]
- database modifications [SQL Server]
- version control [Visual Database Tools]
- Visual Database Tools [SQL Server], multiuser environments
ms.assetid: 330bd48c-9427-4967-b58e-b7c492d5ee36
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1dc9d3d1fca5c3d2ed979f8b6144861ee8256b66
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47716536"
---
# <a name="multiuser-environments-visual-database-tools"></a>多使用者環境 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
在多使用者環境中，其他使用者可以連接並變更您正在使用的相同資料庫。 因此數個使用者可同時使用同一個資料庫物件。 也就是說，當您在多使用者環境中進行變更時，其他使用者所做的變更可能會影響資料庫，反之亦然。  
  
在多使用者環境中使用資料庫的重點即為存取權限。 您具備的資料庫權限將決定您可以使用資料庫的工作範圍。 例如，若要變更資料庫中的物件，您必須擁有資料庫的寫入權限。 如需資料庫權限的詳細資訊，請參閱您的資料庫文件。 如需詳細資訊，請參閱[權限和 Visual Database Tools &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/permissions-and-visual-database-tools-visual-database-tools.md)。  
  
當您儲存對資料表所做的變更時，[資料表設計師] 會驗證自您上次儲存變更以來資料庫沒有被修改過。 如果其他使用者變更該資料庫，您將接獲通知表示資料庫已被修改過。 您可能需要調整這些變更。 如需詳細資訊，請參閱[協調多位使用者所做的變更 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/reconcile-changes-made-by-multiple-users-visual-database-tools.md)。  
  
在多使用者環境中必須注意某些特殊考量，以避免使變更發生衝突。 如需詳細資訊，請參閱[資料庫演進問題 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/issues-of-database-evolution-visual-database-tools.md)。  
  
一個避免問題的方法是，在進行變更時使用資料庫的複本，例如測試資料庫，然後建立變更指令碼 (Change Script)，先在離線時解決衝突後，再於原始資料庫上執行該指令碼，以進行這些變更。 如需詳細資訊，請參閱[開發、測試和生產資料庫 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/development-test-and-production-databases-visual-database-tools.md)。  
  
