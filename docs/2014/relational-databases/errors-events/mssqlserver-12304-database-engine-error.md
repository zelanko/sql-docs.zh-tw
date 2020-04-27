---
title: MSSQLSERVER_12304 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 12304 (Database Engine error)
ms.assetid: a2c252c2-e815-4ac8-a101-7af5b32e3233
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c50e4bdbfe6fd9af1c5e5a6d528a270c0b63c50f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62870206"
---
# <a name="mssqlserver_12304"></a>MSSQLSERVER_12304
    
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|12304|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|HK_UNSUPPORTED_IDENTITY_TABLE_VAR|  
|訊息文字|在原生編譯預存程序的內容之外使用記憶體最佳化資料表類型時，不支援該類型與其任何資料行搭配使用 IDENTITY 屬性。|  
  
## <a name="user-action"></a>使用者動作  
 請勿使用將識別屬性與其任何資料行搭配使用的記憶體最佳化資料表類型。  
  
## <a name="see-also"></a>另請參閱  
 [記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
