from requests import post,get
import urllib.request
import re
upload_ids = []
save = True
def Send(idchat, massage, userchat):
	try:
		if massage == '/start':
				reply = f'Welcome To @{userchat}\nSend Url Video Only\nProgramming By @Br2in'
				url = f"https://api.telegram.org/bot{token}/SendMessage?chat_id={idchat}&text={reply}"
				send = get(url)
		elif 'soundcloud' in massage:
			data = {
				'url': massage
			}
			req = post('https://clouddownloader.net/ajax.php', data=data).text
			p = req.split(' "requested_subtitles": null, "url": "')[1]
			url = p.split('", "ext": "mp3"')[0]
			urllib.request.urlretrieve(url, 'Soundcloud.mp3')
			S = {'document':open('Soundcloud.mp3', 'rb')}
			url = f"https://api.telegram.org/bot{token}/Senddocument?chat_id={idchat}&caption=Welcome Baby"
			send = post(url, files=S).text
		elif 'twitter' in massage:
			data = {
				"URL": massage
			}
			req = post('https://twdown.net/download.php', data=data).text
			L = req.split('download href="')[1]
			url = L.split('target="_blank"')[0]
			urllib.request.urlretrieve(url, 'Twitter.mp4')
			S = {'document':open('Twitter.mp4', 'rb')}
			url = f"https://api.telegram.org/bot{token}/Senddocument?chat_id={idchat}&caption=Welcome Baby"
			send = post(url, files=S).text
		elif 'tiktok' in massage:
			headers = {
				"user-agent": "Mozilla/5.0 (iPhone; CPU iPhone OS 13_2_3 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/13.0.3 Mobile/15E148 Safari/604.1",
				"cookie": "CONSENT=YES+srp.gws-20210526-0-RC2.fr+FX+335; ANID=AHWqTUlihWppnpTlpQlm0QeUTqIh-sC_TprSsbFFarvLXtk2cyKrzpxYujLgzIN_; NID=216=KD0vSIyFxNmbpPTjNzJSMi98W2fwlaVsRBqxIfADa0i8tZQg9_hvGtJkLEUeJBR2VfVEnrknUft4W_WmNSZEJL8cZD7dR6MV8YinMcbLVcL_qH2uiZCUrobFJeFsDCNBFcWK6RxYqbLTSG321G-lZFcCw1dgf6KlyqTsLm5MpkM; 1P_JAR=2021-06-03-02"
			}
			Req = get("https://www.google.com/recaptcha/api2/anchor?ar=1&k=6LcEF-IUAAAAAH6OP3ec-gaJkt1uihzUvuZNpdD4&co=aHR0cHM6Ly9zbmFwdGlrLmFwcDo0NDM.&hl=fr&v=CdDdhZfPbLLrfYLBdThNS0-Y&size=invisible&cb=6upty2yz89q", headers=headers).text
			print(Req)
			q = Req.split('recaptcha-token" value="')[1]
			name = q.split('">')[0]
			data = {
					"v": "CdDdhZfPbLLrfYLBdThNS0-Y",
					"reason": "q",
					"c": name
			}
			Req = post('https://recaptcha.net/recaptcha/api2/reload?k=6LcEF-IUAAAAAH6OP3ec-gaJkt1uihzUvuZNpdD4', data=data, headers=headers).text
			print(Req)
			Captcha = re.compile('rresp","(.*?)"').search(Req)[1]
			headers = {
				"user-agent": "Mozilla/5.0 (iPhone; CPU iPhone OS 13_2_3 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/13.0.3 Mobile/15E148 Safari/604.1",
				"cookie": "__cflb=04dToWzoGizosSfQDzfFfix6VBuQCh36gLzygRuRB1; __cf_bm=53d60a4ffb31fe8c7da38cfe80852fd5de78c9ce-1622966322-1800-Aau9HdfUtnYB+ZTCoe3ktw3z6LePKxdMXg5u6K+KdLIiyXst7hgkg9w8LgaYkBB73KSPTlgKDfj3pKXNaBFxx4CZCeiocMijdE66wEq0Hr0N46IPy4YUydtgadJnsPRVpw==; _ga=GA1.2.1528435556.1622966313; _gid=GA1.2.805902471.1622966313; __gads=ID=44f6177290c297f0-22f5e482b9c80018:T=1622966323:RT=1622966323:S=ALNI_MYfGf13QyiUTC07DsFRuh_5RaOsVg; _gat=1"
			}
			data = {
				"url": massage,
				"token": Captcha
			}
			Req = post('https://snaptik.app/action.php', data=data, headers=headers).text
			V = Req.split("mp4_source','cache_v3')")[1]
			S = V.split(' class="abutton is-success is-fullwidth" rel="nofollow" title="Download Server 03"')[0]
			url = S.split("href='")[1]
			urllib.request.urlretrieve(url, 'TikTok.mp4')
			S = {'document':open('TikTok.mp4', 'rb')}
			url = f"https://api.telegram.org/bot{token}/Senddocument?chat_id={idchat}&caption=Welcome Baby"
			send = post(url, files=S).text
		else:
			data = {
			"link": massage
			}
			req = post('https://sifresiz.instahile.co/downloader', data=data).text
			f = req.split('alt="medya resmi" style="max-height:200px;max-width:100%">')[1]
			i = f.split('<a href="')[1]
			url = i.split('dl=1')[0] + 'dl=1'
			urllib.request.urlretrieve(url, 'iNstagram.mp4')
			S = {'document':open('iNstagram.mp4', 'rb')}
			url = f"https://api.telegram.org/bot{token}/Senddocument?chat_id={idchat}&caption=Welcome Baby"
			send = post(url, files=S).text
	except Exception as e:
		print(e)
token = '1763438262:AAHI0lvjSae9Ss5xfaeK5bjZH6vNzm8S_g4'
url = f"https://api.telegram.org/bot{token}/getUpdates"
while True:
	try:
		Check = get(url)
		JsonCheck = Check.json()
		if save:
			for i in JsonCheck["result"]:
				upload_ids.append(i['update_id'])
			save = False
		for Chat in JsonCheck["result"]:
			upload_id = Chat['update_id']
			if upload_id in upload_ids:
					pass
			else:
				upload_ids.append(upload_id)
				idchat = Chat["message"]["chat"]["id"]
				userchat = Chat["message"]["chat"]["username"]
				massage = Chat["message"]["text"]
				Send(idchat, massage, userchat)
	except Exception as e:
		print(e)
