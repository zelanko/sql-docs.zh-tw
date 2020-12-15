---
description: dbmslpcn.dll 共用記憶體中的 ConnectionValidSharedMemory 函式
title: ConnectionValidSharedMemory dbmslpcn.dll
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 6ae35826-7d75-4542-b686-5f79316b6157
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a487eb380ea4e7b0fe246efdb9281cbab63a1303
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97475989"
---
# <a name="connectionvalidsharedmemory-function-in-dbmslpcndll-shared-memory"></a>dbmslpcn.dll 共用記憶體中的 ConnectionValidSharedMemory 函式
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  此函式會判斷 SQL Server 共用記憶體是否已安裝且正在使用中。  
  
## <a name="syntax"></a>語法  
  
```cpp  
BOOL ConnectionValidSharedMemory(char * szServerName);  
```  
  
## <a name="parameters"></a>參數  
 *szServerName*  
  
-   類型： **char \** _  
  
-   SQL server 的名稱。  
  
## <a name="return-value"></a>傳回值  
 類型： _ *BOOL**  
  
 如果無效，則傳回 0;否則會傳回非零值。  
  
  
