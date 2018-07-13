---
title: bcp_collen |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- bcp_collen
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_collen function
ms.assetid: faaf1f7a-81f2-4852-a178-56602c33673a
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c1d12a0dd303405fd32eec5091d1d7d50e2d7d1f
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37431107"
---
# <a name="bcpcollen"></a>bcp_collen
  設定目前大量複製到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之程式變數中的資料長度。  
  
## <a name="syntax"></a>語法  
  
```  
  
RETCODE bcp_collen (  
HDBC   
hdbc  
,  
DBINT   
cbData  
,  
INT   
idxServerCol  
);  
  
```  
  
## <a name="arguments"></a>引數  
 *hdbc*  
 這是已啟用大量複製的 ODBC 連接控制代碼。  
  
 *cbData*  
 這是資料在程式變數中的長度，不包括任何長度指標或結束字元的長度。 設定*cbData*為 SQL_NULL_DATA 表示複製到伺服器的所有資料列包含資料行的 NULL 值。 將它設定為 SQL_VARLEN_DATA 表示系統將會使用字串結束字元或其他方法來判斷已複製之資料的長度。 如果長度指標與結束字元同時存在，系統會使用造成複製的資料較少的那一個結果。  
  
 *idxServerCol*  
 這是資料表中要將資料複製到其中之資料行的序數位置。 第一個資料行是 1。 資料行的序數位置由報告[SQLColumns](../native-client-odbc-api/sqlcolumns.md)。  
  
## <a name="returns"></a>傳回值  
 SUCCEED 或 FAIL。  
  
## <a name="remarks"></a>備註  
 **Bcp_collen**函式可讓您複製資料時，變更特定資料行之程式變數中的資料長度[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]具有[bcp_sendrow](bcp-sendrow.md)。  
  
 決定資料長度的一開始，當[bcp_bind](bcp-bind.md)呼叫。 如果呼叫之間變更的資料長度**bcp_sendrow**正在使用任何長度前置詞或結束字元，您可以呼叫**bcp_collen**重設長度。 下次呼叫**bcp_sendrow**使用的呼叫所設定的長度**bcp_collen**。  
  
 您必須呼叫**bcp_collen**一次在您想要修改的資料長度的資料表中的每個資料行。  
  
## <a name="see-also"></a>另請參閱  
 [大量複製函數](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
