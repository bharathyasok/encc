# encc
// Includes crypto module 
const crypto = require('crypto'); 
  
const algorithm = 'aes-256-cbc';
const SECRET_KEY = 'Osm!sAw3som3';
const iv = Buffer.alloc(16, 0); 
const key = crypto.scryptSync(SECRET_KEY, 'salt', 32);
function encrypt(Arrval) { 
let encryptArr=[];
  for(const property in Arrval){
	let cipher = crypto.createCipheriv('aes-256-cbc', Buffer.from(key), iv); 

 let encrypted = cipher.update(Arrval[property]); 

 encrypted = Buffer.concat([encrypted, cipher.final()]);  
encryptArr.push({ property : encrypted.toString('hex')}); 
  }
 return encryptArr 
}
function decryptSync(outputObj){
	let decryptArr=[];
  for(const property in outputObj){
    const decipher = crypto.createDecipheriv('aes-256-cbc', Buffer.from(key), iv);
    decipher.update(outputObj[property].property, 'hex');
    decryptArr.push({property : decipher.final('utf8')});
  }
	return decryptArr;
	
};
var output = encrypt({
    username: "root",
    password: "C@l3ido@123"}); 
var output1 = decryptSync(output);
console.log(output);
console.log(output1);


