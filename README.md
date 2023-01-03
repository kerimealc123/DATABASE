# DATABASE

List<Account> multiAcc=new LIst<Account>();
for(Integer num=1;num<=300;num++){
    ACcount singleAcc=new Account();
    singleAcc.Name='bulk Acc-apex' +num;
    multiAcc.add(singleAcc);
}
Account SingleAccError=new Account();
SingleAccError.phone='2222';

multiAcc.add(SingleAccError);
//insert multiAcc;

Database.SaveResult[] srList= Database.insert(multiAcc,false);
for (Database.SaveResult sr : srList) {
    if (sr.isSuccess()) {
        // Operation was successful, so get the ID of the record that was processed
        System.debug('Successfully inserted account. Account ID: ' + sr.getId());
    }
    else {
        // Operation failed, so get all errors                
        for(Database.Error err : sr.getErrors()) {
            System.debug('The following error has occurred.');                    
            System.debug(err.getStatusCode() + ': ' + err.getMessage());
            System.debug('Account fields that affected this error: ' + err.getFields());
        }
    }
}
