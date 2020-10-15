---
description: 變更已註冊之伺服器或已註冊之伺服器群組的名稱
title: 變更已註冊伺服器或伺服器群組的名稱
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 10e1546b-9edb-400c-8676-2ea1192d6134
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 08/02/2016
ms.openlocfilehash: c02287203533d75038a909bd962c9afc70858d2b
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037624"
---
# <a name="change-the-name-of-registered-server-or-registered-server-group"></a>變更已註冊之伺服器或已註冊之伺服器群組的名稱

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 變更 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中已註冊伺服器或伺服器群組的名稱。 該名稱可以隨時變更。 在「已註冊的伺服器」中變更伺服器名稱，僅會變更所顯示的名稱。 若要連接到其他伺服器，您必須編輯已註冊伺服器的連接屬性。  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio

從功能表，巡覽至 [檢視]\\[已註冊的伺服器]**** 開啟 [已註冊的伺服器]**** 窗格。

### <a name="to-change-the-name-of-a-server"></a>變更伺服器的名稱

1. 在 [已註冊的伺服器]**** 中，依序展開 [資料庫引擎]**** 和 [本機伺服器群組]****。  

2. 以滑鼠右鍵按一下伺服器，然後選取 [屬性]**** 開啟 [編輯伺服器註冊屬性]**** 對話方塊視窗。

3. 在 [已註冊的伺服器名稱]**** 文字方塊中，輸入伺服器註冊的新名稱，然後按一下 [儲存]****。  

### <a name="to-change-the-name-of-a-server-group"></a>若要變更伺服器群組名稱  

1. 在 [已註冊的伺服器]**** 中，依序展開 [資料庫引擎]**** 和 [本機伺服器群組]****。  

2. 以滑鼠右鍵按一下伺服器群組，然後選取 [屬性]**** 開啟 [編輯伺服器群組屬性]**** 對話方塊視窗。 

3. 在 [群組名稱]**** 文字方塊中，輸入伺服器群組的新名稱，然後按一下 [儲存]****。  

## <a name="see-also"></a>另請參閱

[變更伺服器的註冊 &#40;SQL Server Management Studio&#41;](./change-a-server-s-registration-sql-server-management-studio.md)