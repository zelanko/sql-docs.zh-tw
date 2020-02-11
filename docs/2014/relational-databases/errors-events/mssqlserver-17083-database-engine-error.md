---
title: MSSQLSERVER_17083 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17083 (Database Engine error)
ms.assetid: 6c83737d-0531-4fd9-88f6-2da5a150532d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c04d010a690d99d90ea3a18ae7f70d33ed39f24b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62915495"
---
# <a name="mssqlserver_17083"></a>MSSQLSERVER_17083
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件識別碼|17083|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|P3_HEKATON_NOT_ATOMIC|  
|訊息文字|原生編譯之預存程序的主體必須是 ATOMIC 區塊。|  
  
## <a name="explanation"></a>說明  
 原生編譯之預存程序的主體沒有 ATOMIC 區塊。  
  
## <a name="user-action"></a>使用者動作  
 原生編譯的預存程序必須包含 ATOMIC 區塊。 例如：  
  
```  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE= N'us_english')  
```  
  
 如需詳細資訊，請參閱[記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。  
  
## <a name="see-also"></a>另請參閱  
 [記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
