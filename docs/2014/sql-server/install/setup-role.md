---
title: 安裝程式角色 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c7e9db15-89f2-4d4d-8860-1e64c5821c4d
caps.latest.revision: 14
author: HeidiSteen
ms.author: heidist
manager: jhubbard
ms.openlocfilehash: b734e817739d887c6e342aa841e3701f770175a6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36033161"
---
# <a name="setup-role"></a>安裝程式角色
  您可以使用此頁面來指定要使用 [特徵選取] 頁面選取個別功能，還是使用安裝程式角色進行安裝。  
  
 `setup role` 是實作預先定義 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態所需之所有功能與共用元件的固定選項。  
  
## <a name="options"></a>選項。  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能安裝**  
 選擇此選項來選取個別功能與共用元件。 執行個體功能包括 Database Engine Services、Analysis Services (原生模式) 和 Reporting Services。  
  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerPivot for SharePoint**  
 選擇此選項將 Analysis Services 伺服器元件安裝在 SharePoint 2010 伺服陣列中。 此選項會在伺服陣列中部署 PowerPivot 系統服務與 Analysis Services 伺服器，讓您針對包含內嵌 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料的已發行 Excel 活頁簿進行查詢與資料處理。  
  
 如果需要關聯式資料庫引擎執行個體以裝載 SharePoint 伺服器陣列的資料庫，可以選擇在安裝中新增關聯式資料庫引擎執行個體。 如果已設定伺服器陣列，您就可以略過此選項。  
  
 安裝完成後，必須使用下列其中一個方法設定軟體：PowerPivot 配置工具、PowerShell 指令程式或 SharePoint 2010 管理中心。 相對於舊版，安裝程式不再執行 PowerPivot 安裝的任何組態工作。  
  
 以角色為基礎的安裝不包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerPivot for Excel 用戶端應用程式。 用戶端應用程式要另外安裝。  
  
 **具有預設值的所有功能**  
 選擇此安裝程式角色來安裝可用於此版本的所有功能。 請注意，這個角色中會排除 PowerPivot for SharePoint。 您必須使用 PowerPivot for SharePoint 安裝程式角色來安裝該功能。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 設定為使用 **NT AUTHORITY\NETWORK SERVICE** 帳戶啟動。 目前的使用者將會當作 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**系統管理員** 角色的成員提供。 此選項所設定的值可透過指定其他命令行參數來覆寫。  
  
 當作業系統不是網域控制站時，Database Engine 和 Reporting Services 預設會使用 NTAUTHORITY\NETWORK SERVICE 帳戶、Integration Services 會使用 NTAUTHORITY\NETWORK SERVICE 帳戶，而 SQL 全文檢索篩選背景程式啟動器則會使用 NTAUTHORITY\LOCAL SERVICE 帳戶。  
  
## <a name="see-also"></a>另請參閱  
 [安裝 PowerPivot for SharePoint](http://go.microsoft.com/fwlink/?LinkId=206906)   
 [硬體和軟體需求 (PowerPivot for SharePoint](http://go.microsoft.com/fwlink/?LinkId=216823)   
 [特徵選取](../../../2014/sql-server/install/feature-selection.md)  
  
  