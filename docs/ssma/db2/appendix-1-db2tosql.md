---
title: 附錄-1 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: c6a30367-d56f-4fcc-8920-c6a6b0335a67
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 70d916526f5b7d7d36c9237624ef311befca39c1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938353"
---
# <a name="appendix---1-db2tosql"></a>附錄-1 (DB2ToSQL)
SSMA 主控台命令列選項的快速檢視：  
  
|Sl。 資料分割|參數|必要項？|參數引數|允許的值|  
|-----------|----------|-------------|-------------------|--------------------|  
|1|-s/script|是|scriptfile|有效的 XML 檔案名稱。<br /><br />主控台指令碼定義檔。|  
|2|-v/變數|否|variablevaluefile|有效的 XML 檔案名稱。<br /><br />如果指令碼檔案中使用變數，則必須指定這個檔案。|  
|3|-c/serverconnection|否|serverconnectionfile|有效的 XML 檔案名稱。<br /><br />此檔案包含伺服器連接資訊。|  
|4|-x/xmloutput|否|xmloutputfile|這個選項表示以 XML 格式的主控台輸出。 如果未指定此選項，預設的輸出是文字格式。<br /><br />如果未指定 xmloutputfile，XML 輸出會導向至 STDOUT。<br /><br />Xmloutputfile 是以 XML 格式的主控台輸出會寫入至其中之檔案的名稱。|  
|5|-l/log|否|logfile|有效的檔案名稱。|  
|6|-e/projectenvironment|否|projectenvironmentfolder|有效的資料夾名稱包含 SSMA 專案環境檔案。|  
|7|-p/securepassword|否|-a/add {<server_id> [,...n] &#124; all} -c&#124;serverconnection  <server-connection-file> [-v&#124;variable <variable-value-file>] [-o/overwrite]<br /><br />或<br /><br />-a/add {<server_id> [,...n] &#124; all} -s&#124;script <script-file> [-v&#124;variable <variable-value-file>] [-o/overwrite]<br /><br />-r/remove {<server_id> [, ...n] &#124; all}<br /><br />-l/list<br /><br />-e/export {<server-id> [, ...n] &#124; all} <encrypted-password -file><br /><br />-i/import {<server-id> [, ...n] &#124; all} <encrypted-password-file>|如果指定，此選項必須不與其他任何選項結合。<br /><br />伺服器識別碼：提供給 {string} 的伺服器唯一識別碼<br /><br />伺服器連線檔案： 伺服器定義檔案 （serverconnectionfile 或指令碼檔案）。<br /><br />變數值檔案：它是變數的定義檔案，並使用伺服器連線檔案中。<br /><br />加密密碼-檔案：這是使用使用者指定的複雜密碼來加密伺服器密碼檔案。|  
|8|-?|否|不適用|不適用|  
  
## <a name="see-also"></a>另請參閱  
[執行 SSMA 主控台](https://msdn.microsoft.com/ce63f633-067d-4f04-b8e9-e1abd7ec740b)  
  
