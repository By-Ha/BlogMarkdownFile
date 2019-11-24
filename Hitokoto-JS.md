title: Hitokoto JS
categories: 编程
tags: [编程]
date: 2019-06-05 18:06:00
---
[原文][1]

```javascript
function initHitokoto() {
	fetch('https://v1.hitokoto.cn/?c=a')
		.then(function(res) {
		  	return res.json();
		})
		.then(function(data) {
		  	var hitokoto = document.getElementById('hitokoto');
		  	hitokoto.innerHTML = '<h2 class="hitokoto-title">一言 ヒトコト<button class="hitokoto-change" onClick="updateHitokoto()"><i class="fas fa-sync-alt"></i>&nbsp;换一换</button></h2><p class="hitokoto-text">' + data.hitokoto + '</p><p class="hitokoto-from">——' + data.from + '</p>';
		})
		.catch(function(err) {
		  	console.error(err);
		});
}

function updateHitokoto() {
	fetch('https://v1.hitokoto.cn/?c=a')
		.then(function(res) {
		  	return res.json();
		})
		.then(function(data) {
			var text = document.getElementsByClassName('hitokoto-text')[0];
			var from = document.getElementsByClassName('hitokoto-from')[0];
			var button = document.getElementsByClassName('hitokoto-change')[0];
			text.setAttribute('style', 'opacity: 0.00;');
			from.setAttribute('style', 'opacity: 0.00;');
			button.setAttribute('style', 'background-color: rgba(146,146,146,1.00); transition:0.2s;');
		  	var hitokoto = document.getElementById('hitokoto');
		  	setTimeout(function() {
				hitokoto.innerHTML = '<h2 class="hitokoto-title">一言 ヒトコト<button class="hitokoto-change" onClick="updateHitokoto()" style="background-color: rgba(146,146,146,1.00); transition:0.2s;"><i class="fas fa-sync-alt"></i>&nbsp;换一换</button></h2><p class="hitokoto-text" style="opacity: 0.00;">' + data.hitokoto + '</p><p class="hitokoto-from" style="opacity: 0.00;">——' + data.from + '</p>';
				setTimeout(function() {
					text = document.getElementsByClassName('hitokoto-text')[0];
					from = document.getElementsByClassName('hitokoto-from')[0];
					button = document.getElementsByClassName('hitokoto-change')[0];
					text.removeAttribute('style');
					from.removeAttribute('style');
					button.removeAttribute('style');
				}, 250);
			}, 250);
		})
		.catch(function(err) {
		  	console.error(err);
		});
}

```


  [1]: https://0and1story.github.io/