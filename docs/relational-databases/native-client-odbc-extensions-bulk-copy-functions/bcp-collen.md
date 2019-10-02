---
title: bcp_collen | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_collen
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_collen function
ms.assetid: faaf1f7a-81f2-4852-a178-56602c33673a
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6cd5a91d3b72b0e3dcd520453373af2d8d4cc33f
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2019
ms.locfileid: "71707713"
---
# <a name="bcp_collen"></a>bcp_collen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  設定目前大量複製到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之程式變數中的資料長度。  
  
## <a name="syntax"></a>語法  
  
```  
  
RETCODE bcp_collen (  
        HDBC hdbc,  
        DBINT cbData,  
        INT idxServerCol);  
```  
  
## <a name="arguments"></a>引數  
 *hdbc*  
 這是已啟用大量複製的 ODBC 連接控制代碼。  
  
 *cbData*  
 這是資料在程式變數中的長度，不包括任何長度指標或結束字元的長度。 將*cbData*設定為 SQL_Null_DATA，表示複製到伺服器的所有資料列都包含資料行的 Null 值。 將它設定為 SQL_VARLEN_DATA 表示系統將會使用字串結束字元或其他方法來判斷已複製之資料的長度。 如果長度指標與結束字元同時存在，系統會使用造成複製的資料較少的那一個結果。  
  
 *idxServerCol*  
 這是資料表中要將資料複製到其中之資料行的序數位置。 第一個資料行是 1。 資料行的序數位置是由[SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md)所報告。  
  
## <a name="returns"></a>傳回值  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>備註  
 **Bcp_collen**函數可讓您在使用[bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)將資料複製到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，針對特定資料行變更程式變數中的資料長度。  
  
 一開始，資料長度是在呼叫[bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)時決定。 如果**bcp_sendrow**的呼叫之間的資料長度變更，且未使用長度前置詞或結束字元，您可以呼叫**bcp_collen**來重設長度。 下一次呼叫**bcp_sendrow**時，會使用**bcp_collen**呼叫所設定的長度。  
  
 您必須針對您想要修改其資料長度的資料表中的每個資料行呼叫**bcp_collen**一次。  
  
## <a name="see-also"></a>另請參閱  
 [大量複製函數](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
