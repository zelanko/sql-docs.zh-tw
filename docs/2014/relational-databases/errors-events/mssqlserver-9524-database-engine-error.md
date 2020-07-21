---
title: MSSQLSERVER_9524 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 9524 (Database Engine error)
ms.assetid: 12da7931-e124-4466-889c-046f1b7b7bfd
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c82132c02376176b5e524f42aadcd343cc40d68b
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553079"
---
# <a name="mssqlserver_9524"></a>MSSQLSERVER_9524
    
## <a name="details"></a>詳細資料  
  
|屬性|值|  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|9254|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|XMLERR_INVALID_COLUMNSET_XML|  
|訊息文字|提供的 XML 內容不符合疏鬆資料行集所需的 XML 格式。|  
  
## <a name="explanation"></a>說明  
 嘗試修改資料行集。 資料行集的 XML 內容必須符合資料行集的格式限制。 資料行集的一般格式如下：  
  
 `<column_name_1>value1</column_name_1><column_name_2>value2</column_name_2>...`  
  
 如需有關資料行集的詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中的＜使用資料行集＞主題。  
  
## <a name="user-action"></a>使用者動作  
 更正陳述式內資料行集的 XML 格式。  
  
  
