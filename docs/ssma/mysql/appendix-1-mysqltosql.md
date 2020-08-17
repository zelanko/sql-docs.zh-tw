---
description: 附錄 - 1 (MySQLToSQL)
title: 附錄-1 (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2d22766d-ff09-420d-ae7c-13b443e28bd0
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: b05a5a6e571179dd5dcd5b1e50368d0b2e16035e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88320644"
---
# <a name="appendix---1-mysqltosql"></a>附錄 - 1 (MySQLToSQL)
SSMA 主控台命令列選項的快速流覽：  
  
|Sl。 否。|參數|必要？|Switch 引數|允許的值|  
|-----------|----------|-------------|-------------------|--------------------|  
|1|-s/腳本|是|scriptfile|有效的 XML 檔案名。<br /><br />主控台腳本定義檔。|  
|2|-v/variable|否|variablevaluefile|有效的 XML 檔案名。<br /><br />如果腳本檔中使用了變數，則必須指定此檔案。|  
|3|-c/serverconnection|否|serverconnectionfile|有效的 XML 檔案名。<br /><br />此檔案包含伺服器連接資訊。|  
|4|-x/xmloutput|否|xmloutputfile|此選項表示以 XML 格式表示的主控台輸出。 如果未指定此選項，預設輸出會是文字格式。<br /><br />如果未指定 xmloutputfile，則會將 XML 輸出導向至 STDOUT。<br /><br />Xmloutputfile 是以 XML 格式寫入主控台輸出的檔案名。|  
|5|-l/log|否|logfile|有效的檔案名。|  
|6|-e/projectenvironment|否|projectenvironmentfolder|包含 SSMA 專案環境檔案的有效資料夾名稱。|  
|7|-p/securepassword|否|-a/add {<server_id> [,.。。n] &#124; all}-c&#124;serverconnection <伺服器-連接檔案> [-v&#124;變數 <變數-值檔案>] [-o/覆寫]<br /><br />或<br /><br />-a/add {<server_id> [,.。。n] &#124; 所有}-s&#124;腳本 <腳本檔> [-v&#124;變數 <變數-值檔案>] [-o/覆寫]<br /><br />-r/remove {<server_id> [，.。。n] &#124; 全部}<br /><br />-l/list<br /><br />-e/export {<server-id> [，.。。n] &#124; all} <加密密碼檔案><br /><br />-i/import {<server-id> [，.。。n] &#124; all} <加密密碼檔案>|如果指定此選項，則此選項不得與任何其他選項結合。<br /><br />伺服器識別碼：為伺服器 {string} 提供的唯一識別碼<br /><br />伺服器-連接檔案：伺服器定義檔 (serverconnectionfile 或 scriptfile) 。<br /><br />變數-值檔案：它是變數定義檔，並用於伺服器連接檔案中。<br /><br />加密密碼檔案：這是使用使用者指定的傳遞片語加密的伺服器密碼檔案。|  
|8|-?|否|不適用|不適用|  
  
## <a name="see-also"></a>另請參閱  
[ (MySQL) 執行 SSMA 主控台 ](https://msdn.microsoft.com/e3e9f7e4-0619-4861-a202-3d5d39953b26)  
  
