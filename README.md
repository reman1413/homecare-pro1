import { useState, useMemo } from "react";

const INIT_NURSES = [
  {id:1,badge:"1510",name:"Ahmed Shajrawi",pos:"NM-Admin",phone:"",email:""},
  {id:2,badge:"101466",name:"Reman Badawood",pos:"HN",phone:"",email:""},
  {id:3,badge:"1249",name:"Maria Eguia",pos:"CN-Admin",phone:"",email:""},
  {id:4,badge:"1798",name:"Maridel Ramilla",pos:"CN-Admin",phone:"",email:""},
  {id:5,badge:"1445",name:"Ahlem Ali Chalbi",pos:"TL Admin",phone:"",email:""},
  {id:6,badge:"1062",name:"Lara Kamel",pos:"TL Admin",phone:"",email:""},
  {id:7,badge:"1438",name:"Crystalline Taga",pos:"HAH-Admin",phone:"",email:""},
  {id:8,badge:"1681",name:"Theresa Millan",pos:"HAH-Admin",phone:"",email:""},
  {id:9,badge:"1540",name:"Wilhelmina Sarraga",pos:"Admin",phone:"",email:""},
  {id:10,badge:"101672",name:"Hoyam Mostafa",pos:"CN-Admin",phone:"",email:""},
  {id:11,badge:"1087",name:"Zorayda Rivera",pos:"RN",phone:"",email:""},
  {id:12,badge:"1363",name:"Nidaa Beddouihech",pos:"RN",phone:"",email:""},
  {id:13,badge:"1192",name:"Farah Naz",pos:"RN",phone:"",email:""},
  {id:14,badge:"1193",name:"Fatimah Kaneez",pos:"RN",phone:"",email:""},
  {id:15,badge:"1199",name:"Neethu Thomas Shiny",pos:"RN",phone:"",email:""},
  {id:16,badge:"1198",name:"Sethulakshmi Sasikumar",pos:"RN",phone:"",email:""},
  {id:17,badge:"1203",name:"Prema Saravanakumar",pos:"RN",phone:"",email:""},
  {id:18,badge:"1204",name:"Prathiba Palanvel",pos:"RN",phone:"",email:""},
  {id:19,badge:"1208",name:"Rajeshwari Marirevaru",pos:"RN",phone:"",email:""},
  {id:20,badge:"1264",name:"Ancy Shamla",pos:"RN",phone:"",email:""},
  {id:21,badge:"1295",name:"Jemima Mary Xavier",pos:"RN",phone:"",email:""},
  {id:22,badge:"1426",name:"Ayesha Khanam",pos:"RN",phone:"",email:""},
  {id:23,badge:"1317",name:"Fathia Fouad",pos:"RN",phone:"",email:""},
  {id:24,badge:"1205",name:"Sangeetha Thilakar",pos:"RN",phone:"",email:""},
  {id:25,badge:"1685",name:"Israa Ahmed Alhussain",pos:"RN",phone:"",email:""},
  {id:26,badge:"1293",name:"Mounika Tholisaku",pos:"RN",phone:"",email:""},
  {id:27,badge:"1296",name:"Amsu Manikandan",pos:"RN",phone:"",email:""},
  {id:28,badge:"1297",name:"Malini Murugan",pos:"RN",phone:"",email:""},
  {id:29,badge:"1298",name:"Lavanya Keelapudi",pos:"RN",phone:"",email:""},
  {id:30,badge:"1423",name:"Bavithra Sekar",pos:"RN",phone:"",email:""},
  {id:31,badge:"1500",name:"Farhat Zeeshan",pos:"RN",phone:"",email:""},
  {id:32,badge:"1723",name:"Amany Abdelnaby",pos:"RN",phone:"",email:""},
  {id:33,badge:"1328",name:"Nathiya Nagappan",pos:"RN",phone:"",email:""},
  {id:34,badge:"1711",name:"Kimberly Dules",pos:"RN",phone:"",email:""},
  {id:35,badge:"1417",name:"Hermia Garcia",pos:"RN",phone:"",email:""},
  {id:36,badge:"1754",name:"Sylvia Yammine",pos:"RN",phone:"",email:""},
  {id:37,badge:"1635",name:"Bimbas Acmed",pos:"RN",phone:"",email:""},
  {id:38,badge:"1634",name:"Rowida Youseif",pos:"RN",phone:"",email:""},
  {id:39,badge:"1465",name:"Simi Chomattil",pos:"RN",phone:"",email:""},
  {id:40,badge:"1450",name:"Gayathri Selvaraj",pos:"RN",phone:"",email:""},
  {id:41,badge:"1458",name:"Krishna Veniparamasivan",pos:"RN",phone:"",email:""},
  {id:42,badge:"1452",name:"Priya Mariyappan",pos:"RN",phone:"",email:""},
  {id:43,badge:"1040",name:"Diana Mae Tardecilla",pos:"RN",phone:"",email:""},
  {id:44,badge:"1425",name:"Peram Navya",pos:"RN",phone:"",email:""},
  {id:45,badge:"1464",name:"Lakshmi Saravanan",pos:"RN",phone:"",email:""},
  {id:46,badge:"1497",name:"Minnu Joseph",pos:"RN",phone:"",email:""},
  {id:47,badge:"1946",name:"Aya Nasser Khater",pos:"RN",phone:"",email:""},
  {id:48,badge:"1948",name:"Dina Ashraf Abdelhalim",pos:"RN",phone:"",email:""},
  {id:49,badge:"1949",name:"Basma Ali Elsayed",pos:"RN",phone:"",email:""},
  {id:50,badge:"1951",name:"Basma Gamal",pos:"RN",phone:"",email:""},
  {id:51,badge:"1952",name:"Amany Yehia",pos:"RN",phone:"",email:""},
  {id:52,badge:"1954",name:"Amira Hamdy",pos:"RN",phone:"",email:""},
  {id:53,badge:"1955",name:"Rewan Elsayed",pos:"RN",phone:"",email:""},
  {id:54,badge:"1957",name:"Esraa Fathy",pos:"RN",phone:"",email:""},
  {id:55,badge:"1959",name:"Mona Ibrahim",pos:"RN",phone:"",email:""},
  {id:56,badge:"1961",name:"Gehan Mostafa",pos:"RN",phone:"",email:""},
  {id:57,badge:"1963",name:"Manar Abdelnaby",pos:"RN",phone:"",email:""},
  {id:58,badge:"101164",name:"Hasan Bilal Al-Kador",pos:"RN",phone:"",email:""},
  {id:59,badge:"101230",name:"Hemavathi Kesava",pos:"RN",phone:"",email:""},
  {id:60,badge:"101220",name:"Sushitha Suresh",pos:"RN",phone:"",email:""},
  {id:61,badge:"101225",name:"Rangeetha Karuppaiya",pos:"RN",phone:"",email:""},
  {id:62,badge:"101415",name:"Meaza Teshome Wordofa",pos:"RN",phone:"",email:""},
  {id:63,badge:"101420",name:"Sri Nursamsiah Nurdin",pos:"RN",phone:"",email:""},
  {id:64,badge:"101422",name:"Kiryana Anblagan",pos:"RN",phone:"",email:""},
  {id:65,badge:"101291",name:"Amal Noordeen Rashed",pos:"RN",phone:"",email:""},
  {id:66,badge:"101517",name:"Glydel May Salise",pos:"RN",phone:"",email:""},
  {id:67,badge:"101521",name:"Cheryll Galas Genovea",pos:"RN",phone:"",email:""},
  {id:68,badge:"101556",name:"Revathy Kalakumari",pos:"RN",phone:"",email:""},
  {id:69,badge:"101555",name:"Devika Sampath",pos:"RN",phone:"",email:""},
  {id:70,badge:"101542",name:"Asha Churchill",pos:"RN",phone:"",email:""},
  {id:71,badge:"101557",name:"Safurabanu Ansar Basha",pos:"RN",phone:"",email:""},
  {id:72,badge:"101608",name:"Janani Rajaram",pos:"RN",phone:"",email:""},
  {id:73,badge:"101612",name:"Nivetha Ayyandurai",pos:"RN",phone:"",email:""},
  {id:74,badge:"101615",name:"Phoebe Younas",pos:"RN",phone:"",email:""},
  {id:75,badge:"101658",name:"Bharathi Subramani",pos:"RN",phone:"",email:""},
  {id:76,badge:"101659",name:"Sarita Raju",pos:"RN",phone:"",email:""},
  {id:77,badge:"101703",name:"Muffy Khoo Esmilla",pos:"AN",phone:"",email:""},
  {id:78,badge:"101704",name:"Priya Embalil Antony",pos:"RN",phone:"",email:""},
  {id:79,badge:"101614",name:"Mosina Parveen",pos:"RN",phone:"",email:""},
  {id:80,badge:"101548",name:"Asanthini Raja",pos:"RN",phone:"",email:""},
  {id:81,badge:"101778",name:"Praba Babu",pos:"RN",phone:"",email:""},
  {id:82,badge:"101783",name:"Suhabana Rashid",pos:"RN",phone:"",email:""},
  {id:83,badge:"101779",name:"Jemuel Casiano",pos:"RN",phone:"",email:""},
  {id:84,badge:"101781",name:"Nurfada Salisa",pos:"RN",phone:"",email:""},
  {id:85,badge:"101733",name:"Siji Mathew",pos:"RN",phone:"",email:""},
  {id:86,badge:"101782",name:"Rhoan Consigna",pos:"RN",phone:"",email:""},
  {id:87,badge:"101788",name:"Shedra Jane Kasim",pos:"RN",phone:"",email:""},
];

const TEAMS = {
  cancellation:{labelAr:"قروب الكنسلتيشن",icon:"❌",color:"#ff6b6b",shifts:[
    {key:"cancel_a",label:"شفت A",time:"8:30ص – 6م",  start:"08:30",end:"18:00",hours:9.5},
    {key:"cancel_b",label:"شفت B",time:"12:30م – 10م",start:"12:30",end:"22:00",hours:9.5},
  ]},
  vaccine:{labelAr:"فريق الفاكسين",icon:"💉",color:"#00c2a8",shifts:[
    {key:"vaccine",label:"شفت ثابت",time:"10ص – 10م",start:"10:00",end:"22:00",hours:12},
  ]},
  phlebotomy:{labelAr:"فريق الفلبوتومي",icon:"🩸",color:"#f0b429",shifts:[
    {key:"phlebo_a",label:"شفت A",time:"6ص – 3م",start:"06:00",end:"15:00",hours:9},
    {key:"phlebo_b",label:"شفت B",time:"يدوي",    start:"",     end:"",     hours:9,manual:true},
  ]},
  nursing:{labelAr:"فريق النيرسنق سيرفس",icon:"🏥",color:"#a78bfa",shifts:[
    {key:"ns_06",label:"6:00ص", start:"06:00",end:"15:00",hours:9},
    {key:"ns_07",label:"7:00ص", start:"07:00",end:"16:00",hours:9},
    {key:"ns_08",label:"8:00ص", start:"08:00",end:"17:00",hours:9},
    {key:"ns_09",label:"9:00ص", start:"09:00",end:"18:00",hours:9},
    {key:"ns_10",label:"10:00ص",start:"10:00",end:"19:00",hours:9},
    {key:"ns_11",label:"11:00ص",start:"11:00",end:"20:00",hours:9},
    {key:"ns_12",label:"12:00م",start:"12:00",end:"21:00",hours:9},
    {key:"ns_13",label:"1:00م", start:"13:00",end:"22:00",hours:9},
    {key:"ns_14",label:"2:00م", start:"14:00",end:"23:00",hours:9},
    {key:"ns_15",label:"3:00م", start:"15:00",end:"00:00",hours:9},
    {key:"ns_16",label:"4:00م", start:"16:00",end:"01:00",hours:9},
    {key:"ns_17",label:"5:00م", start:"17:00",end:"02:00",hours:9},
    {key:"ns_18",label:"6:00م", start:"18:00",end:"03:00",hours:9},
    {key:"ns_19",label:"7:00م", start:"19:00",end:"04:00",hours:9},
    {key:"ns_20",label:"8:00م", start:"20:00",end:"05:00",hours:9},
    {key:"ns_21",label:"9:00م", start:"21:00",end:"06:00",hours:9},
    {key:"ns_22",label:"10:00م",start:"22:00",end:"07:00",hours:9},
    {key:"ns_23",label:"11:00م",start:"23:00",end:"08:00",hours:9},
  ]},
};

const ALL_SHIFTS_FLAT = Object.entries(TEAMS).flatMap(([tk,t])=>
  t.shifts.map(s=>({...s,teamKey:tk,teamIcon:t.icon,teamColor:t.color,teamLabel:t.labelAr}))
);

const CL = [
  {k:"uniform",  cat:"ap",icon:"👗",label:"الزي الرسمي كامل ومرتب"},
  {k:"badge_id", cat:"ap",icon:"🪪",label:"البادج والهوية المؤسسية"},
  {k:"shoes",    cat:"ap",icon:"👟",label:"الحذاء مناسب ونظيف"},
  {k:"hair",     cat:"ap",icon:"💇",label:"الشعر مرتب ومهني"},
  {k:"bag",      cat:"bg",icon:"👜",label:"الحقيبة نظيفة ومرتبة"},
  {k:"gloves",   cat:"bg",icon:"🧤",label:"قفازات طبية كافية"},
  {k:"masks",    cat:"bg",icon:"😷",label:"كمامات كافية"},
  {k:"bp",       cat:"bg",icon:"🩺",label:"جهاز ضغط الدم"},
  {k:"oxi",      cat:"bg",icon:"🩸",label:"مقياس الأكسجين"},
  {k:"scale",    cat:"bg",icon:"⚖️",label:"الميزان / الترمومتر"},
  {k:"forms",    cat:"bg",icon:"📋",label:"النماذج الورقية كاملة"},
  {k:"sanitizer",cat:"bg",icon:"🧴",label:"معقم اليدين"},
  {k:"meds",     cat:"bg",icon:"💊",label:"حقيبة الأدوية الطارئة"},
  {k:"tablet",   cat:"tc",icon:"💻",label:"التابلت موجود وشغال"},
  {k:"battery",  cat:"tc",icon:"🔋",label:"البطارية مشحونة +80%"},
  {k:"app",      cat:"tc",icon:"📱",label:"تطبيق HomeCare مفتوح"},
  {k:"net",      cat:"tc",icon:"📶",label:"الإنترنت يعمل"},
];
const CATS={ap:"👗 المظهر",bg:"👜 الحقيبة",tc:"💻 التقنية"};
const ALL_KEYS=CL.map(i=>i.k);
const TOTAL=ALL_KEYS.length;

const mkNurse = n => ({...n,teamKey:null,shiftKey:null,selfChecks:{},selfSubmitted:false,selfSubmittedAt:null,chargeNotes:"",chargeOverride:{},chargeReviewed:false});

const AV=["#5c7fff","#2ed573","#f0b429","#00c2a8","#a78bfa","#ff6b9d"];
const avC=id=>AV[id%6];
const ini=name=>name.split(" ").slice(0,2).map(w=>w[0]||"").join("").toUpperCase();

function getStatus(n){
  if(!n.selfSubmitted)return"pending";
  const eff={...n.selfChecks,...n.chargeOverride};
  const v=Object.values(eff);
  if(!v.length)return"pending";
  if(v.some(x=>x==="fail"))return"fail";
  if(v.filter(x=>x==="pass").length===TOTAL)return"pass";
  return"partial";
}

const ST={
  pass:   {l:"✅ مكتمل",  c:"#2ed573",bg:"rgba(46,213,115,.13)", bd:"rgba(46,213,115,.3)"},
  fail:   {l:"❌ ملاحظات",c:"#ff4757",bg:"rgba(255,71,87,.13)",  bd:"rgba(255,71,87,.3)"},
  partial:{l:"⚠️ جزئي",  c:"#f0b429",bg:"rgba(240,180,41,.13)", bd:"rgba(240,180,41,.3)"},
  pending:{l:"⏳ انتظار", c:"#7a96c2",bg:"rgba(122,150,194,.1)", bd:"rgba(122,150,194,.25)"},
};

const now=new Date();
const TODAY=`${["الأحد","الاثنين","الثلاثاء","الأربعاء","الخميس","الجمعة","السبت"][now.getDay()]} ${now.getDate()} ${["يناير","فبراير","مارس","أبريل","مايو","يونيو","يوليو","أغسطس","سبتمبر","أكتوبر","نوفمبر","ديسمبر"][now.getMonth()]} ${now.getFullYear()}`;

const BG="#0a1628",S1="#111e35",S2="#162542",BD="rgba(0,194,168,.18)";
const inp={background:S2,border:"1px solid "+BD,borderRadius:8,padding:"8px 11px",color:"#e8f0fe",fontFamily:"inherit",fontSize:13,outline:"none",width:"100%",direction:"rtl"};
const Btn=(bg,c,bd2,extra={})=>({background:bg,border:"1px solid "+(bd2||"transparent"),color:c,padding:"8px 16px",borderRadius:8,cursor:"pointer",fontFamily:"inherit",fontSize:13,fontWeight:600,...extra});

// ── NURSE FORM ───────────────────────────────────────────────
function NurseFormModal({nurse,onSave,onClose}){
  const isEdit=!!nurse;
  const[form,setForm]=useState(nurse?{...nurse}:{name:"",badge:"",pos:"RN",phone:"",email:""});
  const set=(k,v)=>setForm(p=>({...p,[k]:v}));
  const valid=form.name.trim()&&form.badge.trim();
  return(
    <div style={{position:"fixed",inset:0,background:"rgba(0,0,0,.7)",backdropFilter:"blur(4px)",zIndex:400,display:"flex",alignItems:"center",justifyContent:"center",padding:16}}
      onClick={e=>e.target===e.currentTarget&&onClose()}>
      <div style={{background:"#0f2044",border:"1px solid "+BD,borderRadius:16,width:"100%",maxWidth:460,padding:24,direction:"rtl",fontFamily:"Tahoma,Arial,sans-serif",color:"#e8f0fe"}}>
        <div style={{display:"flex",justifyContent:"space-between",alignItems:"center",marginBottom:20}}>
          <div style={{fontSize:16,fontWeight:700}}>{isEdit?"✏️ تعديل بيانات الممرضة":"➕ إضافة ممرضة جديدة"}</div>
          <button onClick={onClose} style={{background:S2,border:"none",color:"#7a96c2",width:28,height:28,borderRadius:7,cursor:"pointer",fontSize:14,fontWeight:700}}>✕</button>
        </div>
        <div style={{display:"grid",gap:12}}>
          <div>
            <div style={{fontSize:11,color:"#7a96c2",marginBottom:5}}>الاسم الكامل *</div>
            <input value={form.name} onChange={e=>set("name",e.target.value)} placeholder="Full Name" style={inp}/>
          </div>
          <div style={{display:"grid",gridTemplateColumns:"1fr 1fr",gap:10}}>
            <div>
              <div style={{fontSize:11,color:"#7a96c2",marginBottom:5}}>رقم الباودج *</div>
              <input value={form.badge} onChange={e=>set("badge",e.target.value)} placeholder="Badge #" style={inp}/>
            </div>
            <div>
              <div style={{fontSize:11,color:"#7a96c2",marginBottom:5}}>المنصب</div>
              <select value={form.pos} onChange={e=>set("pos",e.target.value)} style={{...inp,cursor:"pointer"}}>
                {["RN","HN","AN","CN-Admin","NM-Admin","TL Admin","HAH-Admin","Admin"].map(p=>(
                  <option key={p} value={p}>{p}</option>
                ))}
              </select>
            </div>
          </div>
          <div>
            <div style={{fontSize:11,color:"#7a96c2",marginBottom:5}}>رقم الواتساب</div>
            <input value={form.phone} onChange={e=>set("phone",e.target.value)} placeholder="966XXXXXXXXX" style={inp} dir="ltr"/>
          </div>
          <div>
            <div style={{fontSize:11,color:"#7a96c2",marginBottom:5}}>الإيميل</div>
            <input value={form.email} onChange={e=>set("email",e.target.value)} placeholder="email@meena-health.com" style={inp} dir="ltr"/>
          </div>
        </div>
        <div style={{display:"flex",gap:8,marginTop:20}}>
          <button onClick={()=>valid&&onSave(form)} style={{...Btn(valid?"linear-gradient(135deg,#00c2a8,#00e5cc)":S2,valid?"#0a1628":"#7a96c2"),flex:1,cursor:valid?"pointer":"not-allowed"}}>
            {isEdit?"💾 حفظ التعديلات":"➕ إضافة"}
          </button>
          <button onClick={onClose} style={Btn(S2,"#e8f0fe",BD)}>إلغاء</button>
        </div>
      </div>
    </div>
  );
}

// ── ASSIGN MODAL ─────────────────────────────────────────────
function AssignModal({nurse,onSave,onClose}){
  const[teamKey,setTeamKey]=useState(nurse.teamKey||"");
  const[shiftKey,setShiftKey]=useState(nurse.shiftKey||"");
  const team=TEAMS[teamKey];
  return(
    <div style={{position:"fixed",inset:0,background:"rgba(0,0,0,.7)",backdropFilter:"blur(4px)",zIndex:400,display:"flex",alignItems:"center",justifyContent:"center",padding:16}}
      onClick={e=>e.target===e.currentTarget&&onClose()}>
      <div style={{background:"#0f2044",border:"1px solid "+BD,borderRadius:16,width:"100%",maxWidth:440,padding:24,direction:"rtl",fontFamily:"Tahoma,Arial,sans-serif",color:"#e8f0fe"}}>
        <div style={{display:"flex",justifyContent:"space-between",alignItems:"flex-start",marginBottom:18}}>
          <div>
            <div style={{fontSize:15,fontWeight:700}}>🗓 تعيين الشفت اليومي</div>
            <div style={{fontSize:12,color:"#7a96c2",marginTop:2}}>{nurse.name} · {nurse.badge}</div>
          </div>
          <button onClick={onClose} style={{background:S2,border:"none",color:"#7a96c2",width:28,height:28,borderRadius:7,cursor:"pointer",fontSize:14,fontWeight:700}}>✕</button>
        </div>
        <div style={{marginBottom:14}}>
          <div style={{fontSize:11,color:"#7a96c2",marginBottom:8}}>اختر الفريق</div>
          <div style={{display:"grid",gridTemplateColumns:"1fr 1fr",gap:8}}>
            {Object.entries(TEAMS).map(([k,t])=>(
              <div key={k} onClick={()=>{setTeamKey(k);setShiftKey("");}}
                style={{padding:"10px 12px",borderRadius:9,border:`2px solid ${teamKey===k?t.color:BD}`,background:teamKey===k?t.color+"18":"transparent",cursor:"pointer",transition:"all .15s"}}>
                <div style={{fontSize:18,marginBottom:3}}>{t.icon}</div>
                <div style={{fontSize:12,fontWeight:600,color:teamKey===k?t.color:"#e8f0fe"}}>{t.labelAr}</div>
              </div>
            ))}
          </div>
        </div>
        {team&&(
          <div style={{marginBottom:16}}>
            <div style={{fontSize:11,color:"#7a96c2",marginBottom:8}}>اختر الشفت</div>
            <div style={{display:"grid",gap:6,maxHeight:220,overflowY:"auto"}}>
              {team.shifts.map(s=>(
                <div key={s.key} onClick={()=>setShiftKey(s.key)}
                  style={{padding:"10px 14px",borderRadius:8,border:`2px solid ${shiftKey===s.key?team.color:BD}`,background:shiftKey===s.key?team.color+"15":"transparent",cursor:"pointer",display:"flex",justifyContent:"space-between",alignItems:"center",transition:"all .15s"}}>
                  <div style={{fontSize:13,fontWeight:shiftKey===s.key?700:400,color:shiftKey===s.key?team.color:"#e8f0fe"}}>{s.label}</div>
                  <div style={{fontSize:12,color:"#7a96c2"}}>{s.time||`${s.start} – ${s.end}`}</div>
                </div>
              ))}
              <div onClick={()=>{setTeamKey("");setShiftKey("");}}
                style={{padding:"10px 14px",borderRadius:8,border:"1px solid rgba(255,71,87,.3)",background:"transparent",cursor:"pointer",textAlign:"center",fontSize:12,color:"#ff6b7a",transition:"all .15s"}}>
                🚫 إلغاء التعيين
              </div>
            </div>
          </div>
        )}
        <button onClick={()=>onSave(nurse.id,teamKey,shiftKey)}
          style={{...Btn("linear-gradient(135deg,#00c2a8,#00e5cc)","#0a1628"),width:"100%",opacity:(teamKey&&!shiftKey)?0.5:1,cursor:(teamKey&&!shiftKey)?"not-allowed":"pointer"}}>
          💾 حفظ التعيين
        </button>
      </div>
    </div>
  );
}

// ── CHECKLIST MODAL ──────────────────────────────────────────
function CheckModal({nurse,onSave,onClose}){
  const[checks,setChecks]=useState({...nurse.selfChecks});
  const[notes,setNotes]=useState(nurse.chargeNotes||"");
  const cats=[...new Set(CL.map(i=>i.cat))];
  const answered=k=>checks[k]==="pass"||checks[k]==="fail";
  const pct=Math.round(ALL_KEYS.filter(k=>answered(k)).length/TOTAL*100);
  const done=ALL_KEYS.filter(k=>answered(k)).length;
  return(
    <div style={{position:"fixed",inset:0,background:"rgba(0,0,0,.75)",backdropFilter:"blur(5px)",zIndex:400,display:"flex",alignItems:"center",justifyContent:"center",padding:12}}
      onClick={e=>e.target===e.currentTarget&&onClose()}>
      <div style={{background:"#0f2044",border:"1px solid "+BD,borderRadius:16,width:"100%",maxWidth:520,maxHeight:"90vh",overflowY:"auto",padding:20,direction:"rtl",fontFamily:"Tahoma,Arial,sans-serif",color:"#e8f0fe"}}>
        <div style={{display:"flex",justifyContent:"space-between",alignItems:"flex-start",marginBottom:12}}>
          <div>
            <div style={{fontSize:15,fontWeight:700}}>{nurse.name}</div>
            <div style={{fontSize:11,color:"#7a96c2",marginTop:2}}>{nurse.badge} · {nurse.pos}</div>
          </div>
          <button onClick={onClose} style={{background:S2,border:"none",color:"#7a96c2",width:27,height:27,borderRadius:7,cursor:"pointer",fontSize:13,fontWeight:700}}>✕</button>
        </div>
        <div style={{height:4,background:S2,borderRadius:4,overflow:"hidden",marginBottom:4}}>
          <div style={{height:"100%",background:"linear-gradient(90deg,#00c2a8,#00e5cc)",width:pct+"%",transition:"width .3s"}}/>
        </div>
        <div style={{fontSize:11,color:"#7a96c2",marginBottom:12}}>{done}/{TOTAL} مكتمل</div>
        {cats.map(cat=>(
          <div key={cat} style={{marginBottom:12}}>
            <div style={{fontSize:10,letterSpacing:2,color:"#00c2a8",textTransform:"uppercase",fontWeight:700,marginBottom:6,paddingBottom:4,borderBottom:"1px solid rgba(0,194,168,.15)"}}>{CATS[cat]}</div>
            {CL.filter(i=>i.cat===cat).map(item=>{
              const v=checks[item.k];
              return(
                <div key={item.k} style={{display:"flex",alignItems:"center",justifyContent:"space-between",padding:"7px 10px",background:v==="pass"?"rgba(46,213,115,.06)":v==="fail"?"rgba(255,71,87,.06)":S1,borderRadius:7,marginBottom:3,border:`1px solid ${v==="pass"?"rgba(46,213,115,.2)":v==="fail"?"rgba(255,71,87,.2)":"transparent"}`}}>
                  <span style={{fontSize:12}}>{item.icon} {item.label}</span>
                  <div style={{display:"flex",gap:4}}>
                    {[["pass","✓ موجود","#2ed573","rgba(46,213,115,.15)"],["fail","✗ ناقص","#ff4757","rgba(255,71,87,.15)"]].map(([val,lbl,col,bg])=>(
                      <button key={val} onClick={()=>setChecks(p=>({...p,[item.k]:p[item.k]===val?undefined:val}))}
                        style={{padding:"3px 9px",borderRadius:5,border:`1px solid ${checks[item.k]===val?col+"88":BD}`,background:checks[item.k]===val?bg:"transparent",color:checks[item.k]===val?col:"#7a96c2",cursor:"pointer",fontFamily:"inherit",fontSize:11,fontWeight:700}}>
                        {lbl}
                      </button>
                    ))}
                  </div>
                </div>
              );
            })}
          </div>
        ))}
        <textarea value={notes} onChange={e=>setNotes(e.target.value)} placeholder="ملاحظات إضافية..." rows={2}
          style={{width:"100%",background:S1,border:"1px solid "+BD,borderRadius:8,padding:"8px 11px",color:"#e8f0fe",fontFamily:"inherit",fontSize:12,resize:"none",outline:"none",marginTop:4,direction:"rtl"}}/>
        <div style={{display:"flex",gap:7,marginTop:12}}>
          <button onClick={()=>onSave(nurse.id,checks,notes)} style={{...Btn("linear-gradient(135deg,#00c2a8,#00e5cc)","#0a1628"),flex:1}}>
            💾 حفظ التقييم ({done}/{TOTAL})
          </button>
          <button onClick={onClose} style={Btn(S2,"#e8f0fe",BD)}>إلغاء</button>
        </div>
      </div>
    </div>
  );
}

// ── MAIN ─────────────────────────────────────────────────────
export default function App(){
  const[nurses,setNurses]=useState(()=>{
    try{const s=localStorage.getItem("hcp_v2");return s?JSON.parse(s):INIT_NURSES.map(mkNurse);}
    catch{return INIT_NURSES.map(mkNurse);}
  });
  const[page,setPage]=useState("dashboard");
  const[filterTeam,setFilterTeam]=useState("all");
  const[filterSt,setFilterSt]=useState("all");
  const[q,setQ]=useState("");
  const[nurseForm,setNurseForm]=useState(null);
  const[assignModal,setAssignModal]=useState(null);
  const[checkModal,setCheckModal]=useState(null);
  const[delConfirm,setDelConfirm]=useState(null);
  const[toast,setToast]=useState(null);

  const persist=data=>{setNurses(data);try{localStorage.setItem("hcp_v2",JSON.stringify(data));}catch{}};
  const showToast=msg=>{setToast(msg);setTimeout(()=>setToast(null),3000);};
  const nextId=()=>Math.max(0,...nurses.map(n=>n.id))+1;

  const addNurse=form=>{
    const n=mkNurse({...form,id:nextId()});
    persist([...nurses,n]);
    setNurseForm(null);
    showToast("✅ تمت إضافة "+form.name);
  };
  const editNurse=form=>{
    persist(nurses.map(n=>n.id===form.id?{...n,...form}:n));
    setNurseForm(null);
    showToast("✅ تم تعديل "+form.name);
  };
  const deleteNurse=id=>{
    const n=nurses.find(x=>x.id===id);
    persist(nurses.filter(x=>x.id!==id));
    setDelConfirm(null);
    showToast("🗑 تم حذف "+n?.name);
  };
  const assignShift=(id,teamKey,shiftKey)=>{
    persist(nurses.map(n=>n.id===id?{...n,teamKey:teamKey||null,shiftKey:shiftKey||null}:n));
    setAssignModal(null);
    showToast("✅ تم تعيين الشفت");
  };
  const saveCheck=(id,checks,notes)=>{
    const t=new Date(),ts=`${t.getHours().toString().padStart(2,"0")}:${t.getMinutes().toString().padStart(2,"0")}`;
    persist(nurses.map(n=>n.id===id?{...n,selfChecks:checks,chargeNotes:notes,selfSubmitted:true,selfSubmittedAt:ts,chargeReviewed:true}:n));
    setCheckModal(null);
    showToast("✅ تم حفظ التقييم");
  };
  const exportCSV=()=>{
    const rows=[["الاسم","الباودج","المنصب","الفريق","الشفت","الوقت","الحالة","ملاحظات",...CL.map(i=>i.label)]];
    nurses.forEach(n=>{
      const s=getStatus(n),sh=ALL_SHIFTS_FLAT.find(x=>x.key===n.shiftKey);
      const eff={...n.selfChecks,...n.chargeOverride};
      rows.push([n.name,n.badge,n.pos,sh?.teamLabel||"-",sh?.label||"-",sh?.time||"-",ST[s].l,n.chargeNotes||"-",...CL.map(i=>eff[i.k]==="pass"?"✓":eff[i.k]==="fail"?"✗":"-")]);
    });
    const csv=rows.map(r=>r.map(c=>`"${String(c).replace(/"/g,'""')}"`).join(",")).join("\n");
    const a=document.createElement("a");a.href=URL.createObjectURL(new Blob(["\uFEFF"+csv],{type:"text/csv;charset=utf-8"}));
    a.download=`HomeCare-${now.toISOString().split("T")[0]}.csv`;a.click();
    showToast("📊 تم تصدير التقرير");
  };

  const stats=useMemo(()=>{
    const r={total:nurses.length,pass:0,fail:0,partial:0,pending:0,assigned:0,unassigned:0};
    nurses.forEach(n=>{r[getStatus(n)]++;n.shiftKey?r.assigned++:r.unassigned++;});
    return r;
  },[nurses]);

  const filtered=useMemo(()=>nurses.filter(n=>{
    if(filterTeam==="unassigned")return!n.teamKey;
    if(filterTeam!=="all"&&n.teamKey!==filterTeam)return false;
    if(filterSt!=="all"&&getStatus(n)!==filterSt)return false;
    if(q&&!n.name.toLowerCase().includes(q.toLowerCase())&&!n.badge.includes(q))return false;
    return true;
  }),[nurses,filterTeam,filterSt,q]);

  const stab=a=>({display:"flex",alignItems:"center",gap:8,padding:"9px 13px",cursor:"pointer",borderRight:a?"3px solid #00c2a8":"3px solid transparent",background:a?"rgba(0,194,168,.1)":"transparent",color:a?"#e8f0fe":"#7a96c2",fontSize:12,transition:"all .15s"});
  const pgTab=a=>({padding:"8px 18px",cursor:"pointer",color:a?"#00c2a8":"#7a96c2",fontWeight:a?700:400,fontSize:13,background:"transparent",border:"none",borderBottom:a?"2px solid #00c2a8":"2px solid transparent",fontFamily:"inherit"});

  return(
    <div style={{fontFamily:"Tahoma,Arial,sans-serif",background:BG,color:"#e8f0fe",minHeight:"100vh",direction:"rtl"}}>
      <div style={{position:"fixed",inset:0,backgroundImage:"linear-gradient(rgba(0,194,168,.04) 1px,transparent 1px),linear-gradient(90deg,rgba(0,194,168,.04) 1px,transparent 1px)",backgroundSize:"40px 40px",pointerEvents:"none"}}/>
      {toast&&<div style={{position:"fixed",bottom:22,left:"50%",transform:"translateX(-50%)",background:"#0f2044",border:"1px solid #00c2a8",color:"#e8f0fe",padding:"10px 24px",borderRadius:30,fontWeight:700,fontSize:13,zIndex:999,boxShadow:"0 4px 20px rgba(0,0,0,.4)",whiteSpace:"nowrap"}}>{toast}</div>}
      <div style={{position:"relative",zIndex:1}}>

      {/* Header */}
      <div style={{background:"#0f2044",borderBottom:"1px solid "+BD,padding:"0 18px",height:54,display:"flex",alignItems:"center",justifyContent:"space-between",position:"sticky",top:0,zIndex:50}}>
        <div style={{display:"flex",alignItems:"center",gap:9,fontWeight:700,fontSize:14,color:"#00c2a8"}}>
          <span style={{width:30,height:30,background:"linear-gradient(135deg,#00c2a8,#00e5cc)",borderRadius:7,display:"flex",alignItems:"center",justifyContent:"center",fontSize:15}}>🏥</span>
          HomeCare Pro
        </div>
        <div style={{display:"flex",alignItems:"center",gap:8}}>
          <button onClick={exportCSV} style={Btn("rgba(0,194,168,.12)","#00c2a8","rgba(0,194,168,.3)")}>📊 تصدير</button>
          <span style={{color:"#e8f0fe",fontSize:12}}>{TODAY}</span>
          <span style={{background:"rgba(46,213,115,.12)",border:"1px solid rgba(46,213,115,.3)",color:"#2ed573",padding:"3px 10px",borderRadius:20,fontSize:11,fontWeight:600,display:"flex",alignItems:"center",gap:5}}>
            <span style={{width:5,height:5,background:"#2ed573",borderRadius:"50%",display:"inline-block"}}/>مباشر
          </span>
        </div>
      </div>

      {/* Stats */}
      <div style={{display:"grid",gridTemplateColumns:"repeat(6,1fr)",borderBottom:"1px solid "+BD}}>
        {[{l:"إجمالي",v:stats.total,c:"#e8f0fe"},{l:"معيّنين",v:stats.assigned,c:"#00c2a8"},{l:"غير معيّنين",v:stats.unassigned,c:"#7a96c2"},{l:"مكتمل ✅",v:stats.pass,c:"#2ed573"},{l:"ملاحظات",v:stats.fail+stats.partial,c:"#ff4757"},{l:"انتظار",v:stats.pending,c:"#f0b429"}].map((s,i)=>(
          <div key={i} style={{background:S1,padding:"10px",textAlign:"center",borderLeft:i?"1px solid rgba(0,194,168,.1)":"none"}}>
            <div style={{fontFamily:"monospace",fontSize:20,fontWeight:700,color:s.c,lineHeight:1,marginBottom:2}}>{s.v}</div>
            <div style={{fontSize:10,color:"#7a96c2"}}>{s.l}</div>
          </div>
        ))}
      </div>

      {/* Page tabs */}
      <div style={{background:S1,borderBottom:"1px solid "+BD,padding:"0 18px",display:"flex",gap:4}}>
        <button style={pgTab(page==="dashboard")} onClick={()=>setPage("dashboard")}>📊 لوحة المتابعة</button>
        <button style={pgTab(page==="staff")} onClick={()=>setPage("staff")}>👩‍⚕️ إدارة الموظفين</button>
      </div>

      <div style={{display:"grid",gridTemplateColumns:"200px 1fr",height:"calc(100vh - 122px)"}}>

        {/* Sidebar */}
        <div style={{background:S1,borderLeft:"1px solid "+BD,overflowY:"auto",paddingTop:6}}>
          <div style={{fontSize:9,letterSpacing:2,color:"#7a96c2",textTransform:"uppercase",padding:"8px 13px 4px",fontWeight:700}}>الفرق</div>
          {[
            {k:"all",l:"🔷 الكل",cnt:nurses.length},
            ...Object.entries(TEAMS).map(([k,t])=>({k,l:t.icon+" "+t.labelAr,cnt:nurses.filter(n=>n.teamKey===k).length,c:t.color})),
            {k:"unassigned",l:"⬜ غير معيّن",cnt:stats.unassigned},
          ].map(t=>(
            <div key={t.k} style={stab(filterTeam===t.k)} onClick={()=>setFilterTeam(t.k)}>
              <span style={{flex:1}}>{t.l}</span>
              <span style={{fontFamily:"monospace",fontSize:10,background:S2,padding:"1px 6px",borderRadius:8,color:"#7a96c2"}}>{t.cnt}</span>
            </div>
          ))}
          <div style={{fontSize:9,letterSpacing:2,color:"#7a96c2",textTransform:"uppercase",padding:"11px 13px 4px",fontWeight:700}}>الحالة</div>
          {[{k:"all",l:"الكل"},{k:"pass",l:"✅ مكتمل"},{k:"partial",l:"⚠️ جزئي"},{k:"fail",l:"❌ ملاحظات"},{k:"pending",l:"⏳ انتظار"}].map(f=>(
            <div key={f.k} style={stab(filterSt===f.k)} onClick={()=>setFilterSt(f.k)}>{f.l}</div>
          ))}
        </div>

        {/* Content */}
        <div style={{overflowY:"auto",padding:"14px 16px"}}>

          {/* Search + action bar */}
          <div style={{display:"flex",alignItems:"center",justifyContent:"space-between",marginBottom:14}}>
            <div style={{fontSize:15,fontWeight:700}}>{filtered.length} موظف</div>
            <div style={{display:"flex",gap:8,alignItems:"center"}}>
              <div style={{display:"flex",alignItems:"center",gap:7,background:S2,border:"1px solid "+BD,borderRadius:8,padding:"5px 11px",width:180}}>
                <span style={{color:"#7a96c2"}}>🔍</span>
                <input value={q} onChange={e=>setQ(e.target.value)} placeholder="ابحث..." style={{background:"none",border:"none",outline:"none",color:"#e8f0fe",fontFamily:"inherit",fontSize:13,width:"100%",textAlign:"right",direction:"rtl"}}/>
              </div>
              {page==="staff"&&<button onClick={()=>setNurseForm("new")} style={Btn("linear-gradient(135deg,#00c2a8,#00e5cc)","#0a1628")}>➕ إضافة ممرضة</button>}
            </div>
          </div>

          {/* ── STAFF TABLE ── */}
          {page==="staff"&&(
            <div style={{background:S1,border:"1px solid "+BD,borderRadius:12,overflow:"hidden"}}>
              <div style={{display:"grid",gridTemplateColumns:"34px 1fr 76px 70px 1fr 116px",padding:"9px 13px",background:S2,borderBottom:"1px solid rgba(0,194,168,.12)",fontSize:10,color:"#7a96c2",fontWeight:700,gap:8}}>
                <div>#</div><div>الاسم</div><div>الباودج</div><div>المنصب</div><div>الشفت اليومي</div><div>إجراءات</div>
              </div>
              {filtered.length===0&&<div style={{padding:40,textAlign:"center",color:"#7a96c2"}}>لا توجد نتائج</div>}
              {filtered.map((n,idx)=>{
                const sh=ALL_SHIFTS_FLAT.find(s=>s.key===n.shiftKey);
                return(
                  <div key={n.id} style={{display:"grid",gridTemplateColumns:"34px 1fr 76px 70px 1fr 116px",padding:"10px 13px",borderBottom:"1px solid rgba(0,194,168,.06)",alignItems:"center",gap:8,transition:"background .12s"}}
                    onMouseEnter={e=>e.currentTarget.style.background="rgba(0,194,168,.04)"}
                    onMouseLeave={e=>e.currentTarget.style.background="transparent"}>
                    <div style={{fontFamily:"monospace",fontSize:10,color:"#7a96c2"}}>{idx+1}</div>
                    <div style={{display:"flex",alignItems:"center",gap:7}}>
                      <div style={{width:28,height:28,borderRadius:7,background:avC(n.id)+"22",color:avC(n.id),display:"flex",alignItems:"center",justifyContent:"center",fontSize:10,fontWeight:700,flexShrink:0}}>{ini(n.name)}</div>
                      <div style={{fontSize:12,fontWeight:600,overflow:"hidden",textOverflow:"ellipsis",whiteSpace:"nowrap"}}>{n.name}</div>
                    </div>
                    <div style={{fontFamily:"monospace",fontSize:11,color:"#7a96c2"}}>{n.badge}</div>
                    <div style={{fontSize:11,color:"#7a96c2"}}>{n.pos}</div>
                    <div>
                      {sh
                        ?<span style={{padding:"3px 8px",borderRadius:20,fontSize:11,fontWeight:600,background:sh.teamColor+"18",color:sh.teamColor,border:"1px solid "+sh.teamColor+"44"}}>{sh.teamIcon} {sh.label} · {sh.time||sh.start+"–"+sh.end}</span>
                        :<span style={{fontSize:11,color:"#7a96c2"}}>— غير معيّن</span>}
                    </div>
                    <div style={{display:"flex",gap:4}}>
                      <button onClick={()=>setAssignModal(n)} title="تعيين شفت" style={{width:26,height:26,borderRadius:6,border:"1px solid "+BD,background:"transparent",color:"#00c2a8",cursor:"pointer",fontSize:13}}>🗓</button>
                      <button onClick={()=>setCheckModal(n)} title="تشيك ليست" style={{width:26,height:26,borderRadius:6,border:"1px solid "+BD,background:"transparent",color:"#a78bfa",cursor:"pointer",fontSize:13}}>📋</button>
                      <button onClick={()=>setNurseForm(n)} title="تعديل" style={{width:26,height:26,borderRadius:6,border:"1px solid "+BD,background:"transparent",color:"#f0b429",cursor:"pointer",fontSize:13}}>✏️</button>
                      <button onClick={()=>setDelConfirm(n)} title="حذف" style={{width:26,height:26,borderRadius:6,border:"1px solid rgba(255,71,87,.3)",background:"transparent",color:"#ff4757",cursor:"pointer",fontSize:13}}>🗑</button>
                    </div>
                  </div>
                );
              })}
            </div>
          )}

          {/* ── DASHBOARD CARDS ── */}
          {page==="dashboard"&&(
            <div style={{display:"grid",gridTemplateColumns:"repeat(auto-fill,minmax(255px,1fr))",gap:10}}>
              {filtered.map(n=>{
                const s=getStatus(n),sm=ST[s];
                const sh=ALL_SHIFTS_FLAT.find(x=>x.key===n.shiftKey);
                const eff={...n.selfChecks,...n.chargeOverride};
                const done=ALL_KEYS.filter(k=>eff[k]==="pass").length;
                const pct=n.selfSubmitted?Math.round(done/TOTAL*100):0;
                return(
                  <div key={n.id} style={{background:S1,border:"1px solid "+BD,borderRadius:12,padding:13,transition:"border-color .15s"}}
                    onMouseEnter={e=>e.currentTarget.style.borderColor="#00c2a8"}
                    onMouseLeave={e=>e.currentTarget.style.borderColor=BD}>
                    <div style={{display:"flex",alignItems:"flex-start",justifyContent:"space-between",marginBottom:8}}>
                      <div style={{display:"flex",alignItems:"center",gap:8}}>
                        <div style={{width:30,height:30,borderRadius:7,background:avC(n.id)+"22",color:avC(n.id),display:"flex",alignItems:"center",justifyContent:"center",fontSize:11,fontWeight:700,flexShrink:0}}>{ini(n.name)}</div>
                        <div>
                          <div style={{fontSize:12,fontWeight:600}}>{n.name}</div>
                          <div style={{fontSize:10,color:"#7a96c2",fontFamily:"monospace"}}>{n.badge} · {n.pos}</div>
                        </div>
                      </div>
                      <span style={{padding:"2px 8px",borderRadius:20,fontSize:10,fontWeight:600,background:sm.bg,color:sm.c,border:"1px solid "+sm.bd,whiteSpace:"nowrap"}}>{sm.l}</span>
                    </div>
                    {sh
                      ?<div style={{marginBottom:8}}><span style={{padding:"2px 9px",borderRadius:20,fontSize:11,fontWeight:600,background:sh.teamColor+"18",color:sh.teamColor,border:"1px solid "+sh.teamColor+"44"}}>{sh.teamIcon} {sh.teamLabel} · {sh.label} {sh.time||sh.start+"–"+sh.end}</span></div>
                      :<div style={{marginBottom:8,fontSize:11,color:"#ff6b7a"}}>⚠️ لم يُعيَّن شفت اليوم</div>}
                    {n.selfSubmitted&&(
                      <>
                        <div style={{height:3,background:S2,borderRadius:4,overflow:"hidden",marginBottom:3}}>
                          <div style={{height:"100%",background:s==="pass"?"#2ed573":s==="fail"?"#ff4757":"#f0b429",width:pct+"%",borderRadius:4}}/>
                        </div>
                        <div style={{fontSize:10,color:"#7a96c2",marginBottom:8}}>{done}/{TOTAL} بنود · ⏰ {n.selfSubmittedAt}</div>
                      </>
                    )}
                    <div style={{display:"grid",gridTemplateColumns:"1fr 1fr",gap:5}}>
                      <button onClick={()=>setAssignModal(n)} style={{padding:"6px",background:"rgba(0,194,168,.08)",border:"1px solid rgba(0,194,168,.25)",color:"#00c2a8",borderRadius:7,cursor:"pointer",fontFamily:"inherit",fontSize:11,fontWeight:600}}>🗓 شفت</button>
                      <button onClick={()=>setCheckModal(n)} style={{padding:"6px",background:"rgba(167,139,250,.08)",border:"1px solid rgba(167,139,250,.25)",color:"#a78bfa",borderRadius:7,cursor:"pointer",fontFamily:"inherit",fontSize:11,fontWeight:600}}>📋 تشيك</button>
                    </div>
                    {n.chargeNotes&&<div style={{marginTop:7,background:"rgba(240,180,41,.07)",border:"1px solid rgba(240,180,41,.2)",borderRadius:7,padding:"5px 9px",fontSize:11,color:"#f0b429"}}>💬 {n.chargeNotes}</div>}
                  </div>
                );
              })}
            </div>
          )}
        </div>
      </div>

      {/* Modals */}
      {nurseForm&&<NurseFormModal nurse={nurseForm==="new"?null:nurseForm} onSave={nurseForm==="new"?addNurse:editNurse} onClose={()=>setNurseForm(null)}/>}
      {assignModal&&<AssignModal nurse={assignModal} onSave={assignShift} onClose={()=>setAssignModal(null)}/>}
      {checkModal&&<CheckModal nurse={checkModal} onSave={saveCheck} onClose={()=>setCheckModal(null)}/>}

      {/* Delete confirm */}
      {delConfirm&&(
        <div style={{position:"fixed",inset:0,background:"rgba(0,0,0,.7)",backdropFilter:"blur(4px)",zIndex:400,display:"flex",alignItems:"center",justifyContent:"center",padding:16}}>
          <div style={{background:"#0f2044",border:"1px solid rgba(255,71,87,.3)",borderRadius:14,padding:24,maxWidth:340,width:"100%",textAlign:"center",direction:"rtl",fontFamily:"Tahoma,Arial,sans-serif",color:"#e8f0fe"}}>
            <div style={{fontSize:36,marginBottom:12}}>🗑</div>
            <div style={{fontSize:15,fontWeight:700,marginBottom:6}}>تأكيد الحذف</div>
            <div style={{fontSize:13,color:"#7a96c2",marginBottom:20}}>{delConfirm.name} · {delConfirm.badge}</div>
            <div style={{display:"flex",gap:8,justifyContent:"center"}}>
              <button onClick={()=>deleteNurse(delConfirm.id)} style={Btn("rgba(255,71,87,.15)","#ff4757","rgba(255,71,87,.4)")}>نعم، احذف</button>
              <button onClick={()=>setDelConfirm(null)} style={Btn(S2,"#e8f0fe",BD)}>إلغاء</button>
            </div>
          </div>
        </div>
      )}

      </div>
    </div>
  );
}
