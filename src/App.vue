<!-- 參考網站https://www.ali-nsa.net/zh-tw/explore/alishan -->
<script setup>
    import { reactive, onMounted, ref, onBeforeUnmount } from 'vue'
    const items = reactive([
        {
            title: '認識阿里山',
            photo: './P_alishan/static-title-sm-05.jpg',
            directions: '阿里山國家風景區包括番路、竹崎、梅山、阿里山共四鄉，如葉脈般的交通路網蔓延群山，引領旅人穿梭在層疊的山林綠意，驚豔日出流雲之美、品味細緻茶園風光，還有鄒族原鄉人文，都是阿里山不容錯過的遊憩焦點！',
        },
        {
            title: '氣候地形',
            photo: './P_alishan/ali-img-1-md.jpg',
            subtitle: '氣溫變化大，山勢起伏多',
            directions: '阿里山地區四面高山環繞，氣候涼爽，濕度大、雨量充沛（四月到九月為雨季，十月到翌年三月為旱季），也時常有濃霧，出遊需要特別留意。海拔高度起伏變化大，東部山區屬阿里山山脈，由大塔山、石水山、兜山、萬歲山、塔山、祝山、尖山等二十餘座主要山巒構成，溪流橫貫其間。清水溪上游段因地形起伏，流經岩壁巨石，瀑布景觀特別發達，在瑞峰、瑞里、豐山境內清水溪支流流經處就形成了龍宮、雷音、雲潭、石鼓盤瀑布等景觀。',
        },
        {
            title: '五奇絕景',
            photo: './P_alishan/ali-img-2-md.jpg',
            subtitle: '五奇最經典，來過不錯過',
            directions: '日出、雲海、鐵路、森林、晚霞，提到阿里山，腦海裡浮現的總是脫離不了五奇，當清晨曙光乍現，朝陽輕巧地躍出山頭，為新的一天揭開了序幕，而當傍晚，橙紅西夕又是另一番感動。阿里山雲海名列台灣八景之一，通常出現在天氣晴朗、浮雲遍布的日出或薄暮之時，秋天是觀賞雲海的最佳季節。世界僅存的三條登山鐵路之一就在阿里山，昔日為轉運木材而建，如今蛻變成旅遊列車，載著遊客穿梭在森林間；不想搭火車也能踏上步道親近自然、吸取豐富芬多精，體會高山森林的迷人之處。',
        },
        {
            title: '鄒族風采',
            photo: './P_alishan/ali-img-3-md.jpg',
            subtitle: '訪原民文化，深度遊在地',
            directions: '鄒族在食衣住行育樂均有獨特的脈絡，每年二月舉辦的「Mayasvi（戰祭）」、十月舉行「生命豆季」，保有完整的傳統祭儀，深具文化特色。以茅草為頂的建築，是鄒族獨到的部落景觀，其中又以男子聚會所庫巴「kuba」最具代表性，會所是男子活動中心以及舉辦部落儀式的重要場所，也象徵鄒族文化的宇宙觀與社會觀。而根源於生活所發展出的皮雕、藤編、木雕工藝，十足展現鄒族文化的智慧與美感。',
        },
        {
            title: '山林步道',
            photo: './P_alishan/ali-img-4-md.jpg',
            subtitle: '親近綠生態，盡享森呼吸',
            directions: '沿山麓而上，森林植被隨著海拔高度爬升改變，亞熱帶闊葉林（榕楠林帶）、溫暖闊葉林（楠櫧林帶）、涼溫帶針闊葉混合林（櫟木帶或霧林帶）、冷溫帶山地針葉林（鐵杉林帶）、竹林、山黃麻、樟樹、青剛櫟、紅檜、肖楠、香杉、台灣杉、台灣扁柏、雲杉、鐵杉，不時可以聞到森林樹種所釋放出的獨特香氣，走進樹林感受神清氣爽。冬末夾道迎客的山櫻花登場，揭開了花季的序幕；三月初開始綻放，花期長達一個月的吉野櫻，是阿里山花季的主角；直至暮春，換由桃花出場。這段時間裡，山谷遍野萬紫千紅，宛如世外桃源，一場令人目不暇給的錦簇盛宴，往往贏得駐足讚嘆。',
        },
        {
            title1: '交通部觀光署',
            title2: '阿里山國家風景區管理處',
            title3: '處本部暨觸口遊客中心',
            TEL: '電話：886-5-2593900',
            FAX: '傳真：886-5-2594305',
            ADD: '地址：602037嘉義縣番路鄉觸口村車埕51號',
            gov: './P_alishan/gov.svg',
            photo: './P_alishan/footer-mountain.png'
        }
    ])

    const currentIndex = ref(0)
    let isScrolling = false

    function onWheel(e){
        if (isScrolling) return
        isScrolling = true

        if (e.deltaY > 0 && currentIndex.value < items.length - 1) {
            currentIndex.value++
        } else if (e.deltaY < 0 && currentIndex.value > 0) {
            currentIndex.value--
        }

        setTimeout(() => {
            isScrolling = false
        }, 800)
    }

    onBeforeUnmount(() => {
        window.removeEventListener('wheel', onWheel)
    })

    onMounted(() => {
        window.addEventListener('wheel', onWheel)
        let lastScrollTop = 0
        const navbar = document.querySelector('.navbar')

        window.addEventListener('scroll', () => {
            const scrollTop = window.pageYOffset || document.documentElement.scrollTop
            if (scrollTop > lastScrollTop) {
                // 往下滑，隱藏 navbar
                navbar.style.top = '-80px'
            } else {
                // 往上滑，顯示 navbar
                navbar.style.top = '0'
            }
            lastScrollTop = scrollTop <= 0 ? 0 : scrollTop
        })
    })
</script>

<head>
    
</head>
<template>
    <nav class="navbar navbar-expand-lg fixed-top bg-light shadow">
        <div class="container-fluid">
            <a class="navbar-brand d-flex align-items-center" href="#">
                <img src="/P_alishan/alishanLogo.png" style="height: 48px;">
            </a>
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarSupportedContent">
                <ul class="navbar-nav me-auto mb-2 mb-lg-0" >
                    <li class="nav-item" v-for="item in items" :key="item.title" >
                        <a class="nav-link" :href="`#${item.title}`">{{ item.title }}</a>
                    </li>
                </ul>
            </div>
        </div>
    </nav>
    <div class="scroll-wrapper">
        <div
        class="scroll-container"
        :style="{ transform: `translateY(-${currentIndex * 100}vh)` }"
        >
            <div :id="`${item.title}`" v-for="item in items" :key="item.title" 
                    class="mh-100 bg-cover bg-center text-white d-flex justify-content-center align-items-center text-center"
                    :style="{
                        backgroundImage: `url(${item.photo})`,
                        backgroundSize: 'cover',
                        backgroundPosition: 'center',
                        height: '100vh',
                    }
            ">
                <div class="bg-dark bg-opacity-50 rounded">
                    <div class="fs-1">{{ item.title }}</div>
                    <div>{{ item.directions }}</div>
                    <img :src="item.gov">
                    <div>{{ item.title1 }}</div>
                    <div>{{ item.title2 }}</div>
                    <div>{{ item.title3 }}</div>
                    <div>{{ item.TEL }}</div>
                    <div>{{ item.FAX }}</div>
                    <div>{{ item.ADD }}</div>
                </div>
                </div>

                <div class="mw-100">
            </div>
        </div>
    </div>
</template>

<style>
body::-webkit-scrollbar {
    display: none;
}
.navbar {
  transition: top 0.2s;
}
.scroll-wrapper {
  height: 100vh;
  overflow: hidden;
  position: relative;
  margin-top: 56px; /* 避開 navbar 高度 */
}

.scroll-container {
  transition: transform 0.8s ease-in-out;
}

.item-section {
  height: 100vh;
  background-repeat: no-repeat;
}
</style>