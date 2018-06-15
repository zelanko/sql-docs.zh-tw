---
title: MSSQLSERVER_1803 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 1803 (Database Engine error)
ms.assetid: d4315390-82f1-4c4c-8d1b-1a4989537cca
caps.latest.revision: 17
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c2ea56f5845dca5478ddd16b9a5061cef733fc72
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2018
ms.locfileid: "34319809"
---
# <a name="mssqlserver1803"></a>MSSQLSERVER_1803
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[SQL Server]|  
|事件識別碼|1803|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|NO_SPACE|  
|訊息文字|CREATE DATABASE 失敗。 主要檔案至少要有 %d MB，才能容納模型資料庫的副本。|  
  
## <a name="explanation"></a>說明  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會建立模型資料庫的複本來建立資料庫。 然後 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將此複本重新命名，並將新的資料庫放大為所要求的大小。 在此情況下，使用者嘗試建立小於模型資料庫的資料庫。 由於模型資料庫的複本不適合主要資料檔案 (因為檔案小於此模型資料庫)，所以此作業失敗。  
  
## <a name="user-action"></a>使用者動作  
使用較大的資料庫檔案大小建立資料庫。 然後如果您想要使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 DBCC SHRINKDATABASE 陳述式，請縮小資料庫。  
  
