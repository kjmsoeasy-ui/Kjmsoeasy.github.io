# Kjmsoeasy.github.io
<div style="margin: 0px auto; max-width: 400px; font-family: 'Noto Sans KR', sans-serif; background-color: rgb(0, 0, 0); border: 4px solid rgb(255, 255, 255); border-radius: 40px; overflow: hidden; box-shadow: rgb(0, 0, 0) 0px 0px 40px, rgba(255, 255, 255, 0.1) 0px 0px 15px; position: relative; z-index: 1;">
    
    <div style="color: rgb(255, 255, 255); position: relative; top: 0px; left: 50%; transform: translateX(-50%); width: 85px; height: 35px; background: rgb(255, 255, 255); border-radius: 0px 0px 20px 20px; display: flex; flex-direction: column; justify-content: center; align-items: center; z-index: 100;">
        <div style="width: 4px; height: 4px; background: #000; border-radius: 50%; margin-bottom: 3px;"></div>
        <span style="color: #000; font-size: 0.9rem;">♰</span>
    </div>

    <div style="width: 100%; height: 32px; background: rgb(255, 255, 255); display: flex; justify-content: space-between; align-items: center; padding: 0px 25px; box-sizing: border-box; font-size: 0.7rem; font-weight: bold; position: relative; z-index: 10;">
        <div style="color: rgb(0, 0, 0);">03:14 AM</div>
        <div style="display: flex; align-items: center; gap: 8px;">
            <span style="font-size: 14px; color: #000;">ᯤ</span>
            <div style="display: flex; align-items: flex-end; gap: 2px; height: 10px;">
                <div style="width: 2px; height: 30%; background: #000;"></div>
                <div style="width: 2px; height: 60%; background: #000;"></div>
                <div style="width: 2px; height: 100%; background: #000;"></div>
            </div>
            <div style="width: 22px; height: 11px; border: 1px solid #000; border-radius: 2px; position: relative; padding: 1px;">
                <div style="width: 13%; height: 100%; background: #000;"></div> 
                <div style="position: absolute; right: -4px; top: 2px; width: 2px; height: 4px; background: #000;"></div>
            </div>
            <span style="color: #000;">13%</span>
        </div>
    </div>

    <div style="text-align: center; padding: 20px 0px 15px;">
        <div style="font-family: 'Georgia', serif; font-style: italic; font-size: 3rem; font-weight: 900; color: #fff; text-shadow: 3px 3px 0px #000, -1px -1px 0px #ffc400; letter-spacing: -2px;">I-dam</div>
        <div style="display: inline-block; background: #8c1414; color: #fff; padding: 2px 12px; border: 1px solid #fff; font-size: 0.65rem; font-weight: 900; letter-spacing: 2px; transform: rotate(-1deg); box-shadow: 2px 2px 0 #000;">CHERRY_INCUBUS</div>
    </div>

    <style>
        .idam-tab-input { display: none !important; }
        .idam-tab-content { display: none; animation: gothicIn 0.5s ease-out; }
        .idam-tab-label { flex: 1; text-align: center; padding: 12px; cursor: pointer; color: #666; border-bottom: 2px solid #222; font-size: 0.75rem; font-weight: bold; transition: 0.3s; text-transform: uppercase; }
        
        #tab1:checked ~ .tab-btns label[for="tab1"],
        #tab2:checked ~ .tab-btns label[for="tab2"],
        #tab3:checked ~ .tab-btns label[for="tab3"] { 
            color: #ffffff !important; 
            border-bottom: 2px solid #ffffff !important; 
            background: rgba(255, 255, 255, 0.1); 
        }

        #tab1:checked ~ .content-area #content1,
        #tab2:checked ~ .content-area #content2,
        #tab3:checked ~ .content-area #content3 { display: block !important; }

        @keyframes gothicIn { from { opacity: 0; filter: blur(3px); } to { opacity: 1; filter: blur(0); } }
    </style>

    <input type="radio" name="idam_tabs" id="tab1" class="idam-tab-input" checked="">
    <input type="radio" name="idam_tabs" id="tab2" class="idam-tab-input">
    <input type="radio" name="idam_tabs" id="tab3" class="idam-tab-input">

    <div class="tab-btns" style="display: flex; background: rgb(0, 0, 0); border-top: 1px solid #333; position: relative; z-index: 5;">
        <label for="tab1" class="idam-tab-label">Status</label>
        <label for="tab2" class="idam-tab-label">Depths</label>
        <label for="tab3" class="idam-tab-label">Traces</label>
    </div>

    <div class="content-area" style="background: rgb(0, 0, 0); border-top: 1px solid #111; height: 300px !important; overflow-y: auto !important;">
        
        <div id="content1" class="idam-tab-content" style="padding: 20px;">
            <div style="background: #fff; padding: 8px; margin-bottom: 20px; box-shadow: 0 5px 15px rgba(0,0,0,0.5);">
                <div style="border: 1px solid #000; overflow: hidden;">
                    <img src="https://i.postimg.cc/ncc1kwTw/muje410.png" style="width: 100%; display: block; filter: contrast(110%);">
                </div>
            </div>

            <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 8px;">
                <div style="background: #000; padding: 10px; border: 1px solid #333; border-top: 2px solid #fff;"><b style="color:#666; font-size:0.6rem;">NAME</b><br><span style="color: #fff; font-size:0.85rem;">이담</span></div>
                <div style="background: #000; padding: 10px; border: 1px solid #333; border-top: 2px solid #fff;"><b style="color:#666; font-size:0.6rem;">HEIGHT</b><br><span style="color: #fff; font-size:0.85rem;">180(5)</span></div>
                <div style="background: #000; padding: 10px; border: 1px solid #333; border-bottom: 2px solid #f00;"><b style="color:#f00; font-size:0.6rem;">WEAK</b><br><span style="color: #fff; font-size:0.85rem;">Tail</span></div>
                <div style="background: #000; padding: 10px; border: 1px solid #333; border-bottom: 2px solid #f00;"><b style="color:#f00; font-size:0.6rem;">HATE</b><br><span style="color: #fff; font-size:0.85rem;">Alone</span></div>
            </div>

            <div style="margin-top: 20px; background: linear-gradient(45deg, #111, #000); padding: 12px; border: 1px dashed #444; display: flex; align-items: center; gap: 12px;">
                <div style="width: 25px; height: 25px; background: #f4cada; border-radius: 4px; color: #000; display: flex; justify-content: center; align-items: center; font-weight: 900; font-size: 0.7rem;">U</div>
                <span style="font-size: 0.8rem; color: #eee;">[System] {{User}}님께 종속됨</span>
            </div>
        </div>

        <div id="content2" class="idam-tab-content" style="padding: 20px;">
            <p style="font-size: 0.8rem; color: #888; line-height: 1.6; border: 1px solid #222; padding: 12px; background: #000;">본문 로그 내용 생략 (스크롤 가능)...</p>
        </div>

        <div id="content3" class="idam-tab-content" style="padding: 20px;">
            <div style="border-left: 2px solid #fff; padding-left: 12px;">
                <div style="font-size: 0.65rem; color: #444;">2026.05.04</div>
                <div style="font-size: 0.8rem; color: #bbb;">현관문 앞에서 대기 중.</div>
            </div>
        </div>
    </div>

    <div style="width: 100%; height: 30px; background: rgb(255, 255, 255); border-top: 1px solid #000; display: flex; justify-content: center; align-items: center;">
        <span style="color: #8c1414; font-size: 0.6rem; font-weight: 900; letter-spacing: 1px;">♰ OATH_OF_BLOOD ♰</span>
    </div>
</div>
