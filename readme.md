## Enable creation and removal of extension via base MySQL. Issabel 4/Asterisk 16

-- In the PABX

1. Edit the file /etc/asterisk/res_config_mysql.conf, uncommenting the lines dbuser and dbpass. 

2. adjust the fields dbuser and dbpass for the credentials to access the base. as below.
dbuser = asterisk
dbpass = 1234

3. Activate extension data update via bank. editing the file /etc/asterisk/extconfig.conf, uncommenting the sipeers line. As below.
sippeers => odbc,asterisk

-- # in the Base MySQL

-- create new user 
CREATE USER 'asterisk'@'*' IDENTIFIED BY '1234';
SET PASSWORD FOR asterisk@'%'=PASSWORD('1234');
GRANT ALL PRIVILEGES ON *.* TO 'asterisk'@'%';
FLUSH PRIVILEGES;

--  Create extension registration table
DROP TABLE IF EXISTS asterisk.`sippeers`; 
CREATE TABLE asterisk.`sippeers` (
    `id` int(11) NOT NULL AUTO_INCREMENT,
    `name` varchar(10) COLLATE utf8mb4_unicode_ci NOT NULL,
    `ipaddr` varchar(15) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `port` int(5) DEFAULT NULL,
    `regseconds` int(11) DEFAULT NULL,
    `defaultuser` varchar(10) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `fullcontact` varchar(35) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `regserver` varchar(20) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `useragent` varchar(20) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `lastms` int(11) DEFAULT NULL,
    `host` varchar(40) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `type` enum('friend','user','peer') COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `context` varchar(40) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `permit` varchar(40) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `deny` varchar(40) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `secret` varchar(40) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `md5secret` varchar(40) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `remotesecret` varchar(40) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `transport` enum('udp','tcp','udp,tcp','tcp,udp') COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `dtmfmode` enum('rfc2833','info','shortinfo','inband','auto') COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `directmedia` enum('yes','no','nonat','update') COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `nat` enum('yes','no','never','route') COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `callgroup` varchar(40) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `pickupgroup` varchar(40) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `language` varchar(40) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `allow` varchar(40) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `disallow` varchar(40) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `insecure` varchar(40) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `trustrpid` enum('yes','no') COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `progressinband` enum('yes','no','never') COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `promiscredir` enum('yes','no') COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `useclientcode` enum('yes','no') COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `accountcode` varchar(40) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `setvar` varchar(40) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `callerid` varchar(40) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `amaflags` varchar(40) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `callcounter` enum('yes','no') COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `busylevel` int(11) DEFAULT NULL,
    `allowoverlap` enum('yes','no') COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `allowsubscribe` enum('yes','no') COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `videosupport` enum('yes','no') COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `maxcallbitrate` int(11) DEFAULT NULL,
    `rfc2833compensate` enum('yes','no') COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `mailbox` varchar(40) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `session-timers` enum('accept','refuse','originate') COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `session-expires` int(11) DEFAULT NULL,
    `session-minse` int(11) DEFAULT NULL,
    `session-refresher` enum('uac','uas') COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `t38pt_usertpsource` varchar(40) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `regexten` varchar(40) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `fromdomain` varchar(40) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `fromuser` varchar(40) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `qualify` varchar(40) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `defaultip` varchar(40) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `rtptimeout` int(11) DEFAULT NULL,
    `rtpholdtimeout` int(11) DEFAULT NULL,
    `sendrpid` enum('yes','no') COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `outboundproxy` varchar(40) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `callbackextension` varchar(40) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `timert1` int(11) DEFAULT NULL,
    `timerb` int(11) DEFAULT NULL,
    `qualifyfreq` int(11) DEFAULT NULL,
    `constantssrc` enum('yes','no') COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `contactpermit` varchar(40) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `contactdeny` varchar(40) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `usereqphone` enum('yes','no') COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `textsupport` enum('yes','no') COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `faxdetect` enum('yes','no') COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `buggymwi` enum('yes','no') COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `auth` varchar(40) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `fullname` varchar(40) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `trunkname` varchar(40) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `cid_number` varchar(40) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `callingpres` enum('allowed_not_screened','allowed_passed_screen','allowed_failed_screen','allowed','prohib_not_screened','prohib_passed_screen','prohib_failed_screen','prohib') COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `mohinterpret` varchar(40) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `mohsuggest` varchar(40) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `parkinglot` varchar(40) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `hasvoicemail` enum('yes','no') COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `subscribemwi` enum('yes','no') COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `vmexten` varchar(40) COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `autoframing` enum('yes','no') COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `rtpkeepalive` int(11) DEFAULT NULL,
    `call-limit` int(11) DEFAULT NULL,
    `g726nonstandard` enum('yes','no') COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `ignoresdpversion` enum('yes','no') COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `allowtransfer` enum('yes','no') COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    `dynamic` enum('yes','no') COLLATE utf8mb4_unicode_ci DEFAULT NULL,
    PRIMARY KEY (`id`),
    UNIQUE KEY `name` (`name`),
    KEY `ipaddr` (`ipaddr`,`port`),
    KEY `host` (`host`,`port`)
) ENGINE=InnoDB AUTO_INCREMENT=5 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;

-- Insert new extension
INSERT INTO asterisk.sippeers
	(name, secret, host, context)
VALUES
	('6001', '6001', 'dynamic', 'from-internal');

Obs. remember to change the username and password of the extension and, if necessary, the context



