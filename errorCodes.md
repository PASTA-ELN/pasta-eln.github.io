automatically created MD file of error codes by miscTools:errorCodesp
# database.py
  - dit01: Something unexpected has happend+traceback.format_exc(
    Likely userName / password not correct
 : could not update document. Likely version conflict. Initial and current version:'
  - dgv01: Database / Network problem for path |',thePath
  - dsv01: something unexpected has happend. Log-file has traceback'
  - drp01: Could not connect to remote server. Abort replication.'
  - drp02: replicate error |\n",traceback.format_exc(
  - dch01: branch does not exist '+doc['_id']
  - dch02: branch length >1 for text'+doc['_id']+' '+str(doc['-type']
  - dch03: non-text in stack '+doc['_id']
  - dch04: no type in '+doc['_id']
  - dch05: child-number and dirName dont match '+doc['_id']
  - dch06: branch path is None '+doc['_id']
  - dch07: branch not in parent with id '+parentID
  - dch08: parent does not have corresponding path '+doc['_id']+'| parentID '+parentID
  - dch17: name not in '+doc['_id']
  - dch09: qrCode not in sample '+doc['_id']
  - dch10: shasum not in measurement '+doc['_id']
  - dch11: image not in measurement '+doc['_id']
  - dch12: jpg-image not valid '+doc['_id']
  - dch13: svg-image not valid '+doc['_id']
  - dch14: image not valid '+doc['_id']+' '+doc['image']
  - dch15: critical error in '+doc['_id']
  - dch16: shasum twice in view: '+key+' '+item['id']+' '+item['value']

# backend.py
  Configuration version does not fit'
  - bin01: Base folder did not exist |'+self.basePath
  - bad01: fetch remote content failed. Data not added'
  - bad02: Tried to create new datalad folder which did already exist'
  - bch01: Could not change into hierarchy. id|'+docID+'  directory:'+dirName+'  cwd:'+self.cwd
  - bbu02: document not in zip file |",doc['_id']
  - bbu03: revision not in zip file |",attachmentName
  - brp01: You tried to replicate although, remote is not defined"
  - bse01: doc path was not found and parent path was not found |"+doc
  - bgc01: No hierarchy tree'

# pastaELN.py
  - pma01: CouchDB server not working |',url
  - pma01a: Wrong local server.' from None
  - pma20: backend could not be started.+traceback.format_exc(+'\n
  - pma02: Ontology does NOT exist on server'
  - pma03: syncRL not implemented yet'
  - pma06: error after redo-extraction'
  - pma07: something strange occurs with content string'
  - pma08: command in pastaELN.py does not exist |",args.command
  - pma09: undefined'
  - pma10: exception thrown during pastaELN.py"+traceback.format_exc(+"\n"

# miscTools.py
  - mpq01: Printing error'
  - mcc01a: No softwareDir in config file
    Click *MAINTENANCE* and *AUTOMATICALLY REPAIR CONFIGURATION*
  - mcc01b: No userID in config file
    Click *MAINTENANCE* and *AUTOMATICALLY REPAIR CONFIGURATION*
  - mcc01d: No magicTags in config file
    Click *MAINTENANCE* and *AUTOMATICALLY REPAIR CONFIGURATION*
  - mcc01e: No qrPrinter in config file
    Click *MAINTENANCE* and *AUTOMATICALLY REPAIR CONFIGURATION*
  - mcc01f: No tableFormat in config file
    Click *MAINTENANCE* and *AUTOMATICALLY REPAIR CONFIGURATION*
  - mcc01g: No extractors in config file
    Click *MAINTENANCE* and *AUTOMATICALLY REPAIR CONFIGURATION*
  - mcc01h: No or wrong version in config file
    Click *MAINTENANCE* and *AUTOMATICALLY REPAIR CONFIGURATION*
  - mcc01j: No links in config file; REPAIR MANUALLY
    Click *MAINTENANCE* and *AUTOMATICALLY REPAIR CONFIGURATION*
  - mcc01k: No default links in config file
    Click *MAINTENANCE* and *AUTOMATICALLY REPAIR CONFIGURATION*
  - mcc01i: default entry '+conf['default']+' not in links
    Click *MAINTENANCE* and *AUTOMATICALLY REPAIR CONFIGURATION*
  - mcc01l: - type entries '+str(illegalNames+' in config file
    Click *MAINTENANCE* and *AUTOMATICALLY REPAIR CONFIGURATION*

# serverActions.py
  1: put not successful",resp.reason
  2: post not successful",resp.reason
  3: post not successful",resp.reason
  4: post not successful",resp.reason
 : get not successful",resp.reason
 : get not successful",resp.reason
 ** security'
 ** authentication',respI
 : Server cannot be reached"
 : ",write,read,authen,iDB
 : Database cannot be read"
 : Authentication  cannot be read"

