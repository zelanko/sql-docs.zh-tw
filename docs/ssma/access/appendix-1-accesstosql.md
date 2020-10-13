---
description: '附錄-1 (AccessToSQL) '
title: 附錄-1 (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 00665e16-2990-4bfc-8e17-d97ca9fb4999
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 88b8566b0ed3b264f09f0307251dcf9e69270e19
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987668"
---
# <a name="appendix---1-accesstosql"></a>附錄-1 (AccessToSQL) 
SSMA 主控台命令列選項的快速流覽：  
  
|Sl。 不可以。|參數|必要？|Switch 引數|允許的值|  
|-----------|----------|-------------|-------------------|--------------------|  
|1|-s/腳本|是|scriptfile|有效的 XML 檔案名。<br /><br />主控台腳本定義檔。|  
|2|-v/variable|否|variablevaluefile|有效的 XML 檔案名。 如果腳本檔中使用了變數，則必須指定此檔案。|  
|3|-c/serverconnection|否|serverconnectionfile|有效的 XML 檔案名。 此檔案包含伺服器連接資訊。|  
|4|-x/xmloutput|否|xmloutputfile|此選項表示以 XML 格式表示的主控台輸出。 如果未指定此選項，預設輸出會是文字格式。<br /><br />如果未指定 xmloutputfile，則會將 XML 輸出導向至 STDOUT。<br /><br />Xmloutputfile 是以 XML 格式寫入主控台輸出的檔案名。|  
|5|-l/log|否|logfile|有效的檔案名。|  
|6|-e/projectenvironment|否|projectenvironmentfolder|包含 SSMA 專案環境檔案的有效資料夾名稱。|  
|7|-p/securepassword|否|-a/add {<server_id> [,.。。n] &#124; all}-c&#124;serverconnection <伺服器-連接檔案> [-v&#124;變數 <變數-值檔案>] [-o/覆寫]<br /><br />或<br /><br />-a/add {<server_id> [,.。。n] &#124; 所有}-s&#124;腳本 <腳本檔> [-v&#124;變數 <變數-值檔案>] [-o/覆寫]<br /><br />-r/remove {<server_id> [，.。。n] &#124; 全部}<br /><br />-l/list<br /><br />-e/export {<server-id> [，.。。n] &#124; all} <加密密碼檔案><br /><br />-i/import {<server-id> [，.。。n] &#124; all} <加密密碼檔案>|如果指定此選項，則此選項不得與任何其他選項結合。<br /><br />伺服器識別碼：為伺服器 {string} 提供的唯一識別碼<br /><br />伺服器-連接檔案：伺服器定義檔 (serverconnectionfile 或 scriptfile) 。<br /><br />變數-值檔案：它是變數定義檔，並用於伺服器連接檔案中。<br /><br />加密密碼檔案：這是使用使用者指定的傳遞片語加密的伺服器密碼檔案。|  
|8|-?|否|不適用|不適用|  
  
## <a name="see-also"></a>另請參閱  
[執行 SSMA 主控台 (存取) ](./executing-the-ssma-console-accesstosql.md)  
