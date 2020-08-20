---
description: bcp_columns
title: bcp_columns |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_columns
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_columns function
ms.assetid: 5376f6fe-9508-439a-8c66-778d77f19ac3
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9b8e0798ce0b00256923d7740cb450e2949b20ff
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499260"
---
# <a name="bcp_columns"></a>bcp_columns
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  設定在使用者檔案中可搭配大量複製在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中進出作業的資料行總數。 [bcp_setbulkmode](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-setbulkmode.md) 可以用來取代 bcp_columns 和 [bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
RETCODE bcp_columns (  
        HDBC hdbc,  
        INT nColumns);  
```  
  
## <a name="arguments"></a>引數  
 *hdbc*  
 這是已啟用大量複製的 ODBC 連接控制代碼。  
  
 *nColumns*  
 這是使用者檔案中的資料行總數。 即使您準備要將使用者檔案中的資料大量複製到資料表， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 而不想複製使用者檔案中的所有資料行，您仍然必須將 *nColumns* 設定為使用者檔案資料行總數。  
  
## <a name="returns"></a>傳回  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>備註  
 只有使用有效的檔案名呼叫 [bcp_init](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md) 之後，才能呼叫此函數。  
  
 只有打算使用與預設值不同的使用者檔案格式時，才可以呼叫此函數。 如需預設使用者檔案格式之描述的詳細資訊，請參閱 **bcp_init**。  
  
 在呼叫 **bcp_columns**之後，您必須針對使用者檔案中的每個資料行呼叫 [bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md) ，以完整定義自訂檔案格式。  
  
## <a name="see-also"></a>另請參閱  
 [大量複製函數](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
