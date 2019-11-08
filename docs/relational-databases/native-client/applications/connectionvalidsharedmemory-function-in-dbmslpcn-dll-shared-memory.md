---
title: Dbmslpcn .dll 共用記憶體中的 ConnectionValidSharedMemory 函式 |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 6ae35826-7d75-4542-b686-5f79316b6157
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 88f9b581bbe8647981f1828eea70150674039188
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/07/2019
ms.locfileid: "73770769"
---
# <a name="connectionvalidsharedmemory-function-in-dbmslpcndll-shared-memory"></a>dbmslpcn.dll 共用記憶體中的 ConnectionValidSharedMemory 函式
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  函式會判斷是否已安裝和使用 SQL Server 的共用記憶體。  
  
## <a name="syntax"></a>語法  
  
```cpp  
BOOL ConnectionValidSharedMemory(char * szServerName);  
```  
  
## <a name="parameters"></a>參數  
 *szServerName*  
  
-   類型： **char\***  
  
-   SQL server 的名稱。  
  
## <a name="return-value"></a>傳回值  
 類型： **BOOL**  
  
 如果無效，則傳回 0;否則會傳回非零值。  
  
  
