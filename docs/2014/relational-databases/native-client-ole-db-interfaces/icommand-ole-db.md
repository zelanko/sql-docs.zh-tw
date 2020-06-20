---
title: ICommand (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ICommand [SQL Server Native Client]
ms.assetid: 5e24b3a0-0658-44fc-b653-f4c52f9eb328
author: rothja
ms.author: jroth
ms.openlocfilehash: 03bdccc83a04078210f2283d0b330f237ed02979
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85056174"
---
# <a name="icommand-ole-db"></a>ICommand (OLE DB)
  本主題討論 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 特有的 OLE DB 行為。  
  
## <a name="icommandexecute"></a>ICommand::Execute  
 插入大於資料行大小的資料通常會產生錯誤。 不過，在一些狀況下會傳回 S_OK，但是會將 *dwStatus* 設定為 DBSTATUS_S_TRUNCATED。 使用參數插入資料時，如果資料行不夠大，無法保存資料而且尚未呼叫 `ICommandWithParameters::SetParameterInfo`，通常會發生這種情況。  
  
## <a name="see-also"></a>另請參閱  
 [介面 &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)  
  
  
