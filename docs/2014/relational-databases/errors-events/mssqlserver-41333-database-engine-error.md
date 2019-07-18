---
title: MSSQLSERVER_41333 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 41333 (Database Engine error)
ms.assetid: c3c3ae9a-1e4c-4de6-ba72-2f393375b053
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ab94977bcd3bf5a9b0b26ac7be76cb67d58e0755
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62913984"
---
# <a name="mssqlserver41333"></a>MSSQLSERVER_41333
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件識別碼|41333|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|CROSS_CONTAINER_ISOLATION_FAILURE|  
|訊息文字|下列交易必須在快照集隔離下，存取記憶體最佳化資料表和原生編譯的預存程序:RepeatableRead 交易、Serializable 交易，以及存取未在 RepeatableRead 或 Serializable 隔離中進行記憶體最佳化之資料表的交易。|  
  
## <a name="explanation"></a>說明  
 針對在磁碟基礎的交易和 XTP 交易之間較高的隔離等級使用者，有些限制。  
  
## <a name="user-action"></a>使用者動作  
 請勿嘗試在記憶體最佳化的資料表 (和原生編譯程序) 和磁碟基礎的資料表上執行高等級的隔離作業。  
  
 如需詳細資訊，請參閱[記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。  
  
## <a name="see-also"></a>另請參閱  
 [記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
