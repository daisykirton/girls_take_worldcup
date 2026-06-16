const supabase = window.supabase.createClient(
  'https://uumxusprugyifvyipdeq.supabase.co',
  'sb_publishable_XvH0YeSMtyvCjBi_OxxZsQ_i4lsQeJE'
);

const people = [
  {name:'Daisy', teams:['Uruguay','Ecuador','England','Haiti','France']},
  {name:'Frankie', teams:['Jordan','Cabo Verde','Ghana','Bosnia and Herzegovina','USA','Argentina']},
  {name:'Ruby', teams:['Switzerland','Norway','Colombia','Bosnia and Herzegovina','IR Iran']},
  {name:'Charlotte', teams:['Congo DR','Iraq','South Africa','Mexico','Portugal','Paraguay','Japan']},
  {name:'Nicole', teams:['Scotland','Turkiye','Uzbekistan','Curacao','Morocco']},
  {name:'Jade', teams:['Netherlands','Belgium','Brazil','South Korea','Austria']},
  {name:'Eliza', teams:['Germany','Tunisia','Czechia','Algeria','New Zealand']},
  {name:'Lulu', teams:['Senegal','Australia','Canada','Sweden','Qatar']},
  {name:'Darcy', teams:["Cote d'Ivoire",'Egypt','Croatia','Panama','Spain','Saudi Arabia']}
];

const codes = {'Uruguay':'UY','Ecuador':'EC','England':'GB-ENG','Haiti':'HT','France':'FR','Jordan':'JO','Cabo Verde':'CV','Ghana':'GH','Bosnia and Herzegovina':'BA','USA':'US','Argentina':'AR','Switzerland':'CH','Norway':'NO','Colombia':'CO','IR Iran':'IR','Congo DR':'CD','Iraq':'IQ','South Africa':'ZA','Mexico':'MX','Portugal':'PT','Paraguay':'PY','Japan':'JP','Scotland':'GB-SCT','Turkiye':'TR','Uzbekistan':'UZ','Curacao':'CW','Morocco':'MA','Netherlands':'NL','Belgium':'BE','Brazil':'BR','South Korea':'KR','Austria':'AT','Germany':'DE','Tunisia':'TN','Czechia':'CZ','Algeria':'DZ','New Zealand':'NZ','Senegal':'SN','Australia':'AU','Canada':'CA','Sweden':'SE','Qatar':'QA',"Cote d'Ivoire":'CI','Egypt':'EG','Croatia':'HR','Panama':'PA','Spain':'ES','Saudi Arabia':'SA'};

let fixtures = [
 {date:'2026-06-12T05:00:00+10:00', stage:'Group A', group:'A', home:'Mexico', away:'South Africa', venue:'Mexico City'},
 {date:'2026-06-12T12:00:00+10:00', stage:'Group A', group:'A', home:'South Korea', away:'Czechia', venue:'Guadalajara'},
 {date:'2026-06-13T05:00:00+10:00', stage:'Group B', group:'B', home:'Canada', away:'Bosnia and Herzegovina', venue:'Toronto'},
 {date:'2026-06-13T11:00:00+10:00', stage:'Group D', group:'D', home:'USA', away:'Paraguay', venue:'Los Angeles'},
 {date:'2026-06-14T05:00:00+10:00', stage:'Group B', group:'B', home:'Qatar', away:'Switzerland', venue:'San Francisco'},
 {date:'2026-06-14T08:00:00+10:00', stage:'Group C', group:'C', home:'Brazil', away:'Morocco', venue:'New York/NJ'},
 {date:'2026-06-14T11:00:00+10:00', stage:'Group C', group:'C', home:'Haiti', away:'Scotland', venue:'Boston'},
 {date:'2026-06-14T14:00:00+10:00', stage:'Group D', group:'D', home:'Australia', away:'Turkiye', venue:'Vancouver'},
 {date:'2026-06-15T03:00:00+10:00', stage:'Group E', group:'E', home:'Germany', away:'Curacao', venue:'Houston'},
 {date:'2026-06-15T06:00:00+10:00', stage:'Group F', group:'F', home:'Netherlands', away:'Japan', venue:'Dallas'},
 {date:'2026-06-15T09:00:00+10:00', stage:'Group E', group:'E', home:"Cote d'Ivoire", away:'Ecuador', venue:'Philadelphia'},
 {date:'2026-06-15T12:00:00+10:00', stage:'Group F', group:'F', home:'Sweden', away:'Tunisia', venue:'Monterrey'},
 {date:'2026-06-16T02:00:00+10:00', stage:'Group H', group:'H', home:'Spain', away:'Cabo Verde', venue:'Atlanta'},
 {date:'2026-06-16T05:00:00+10:00', stage:'Group G', group:'G', home:'Belgium', away:'Egypt', venue:'Seattle'},
 {date:'2026-06-16T08:00:00+10:00', stage:'Group H', group:'H', home:'Saudi Arabia', away:'Uruguay', venue:'Miami'},
 {date:'2026-06-16T11:00:00+10:00', stage:'Group G', group:'G', home:'IR Iran', away:'New Zealand', venue:'Los Angeles'},
 {date:'2026-06-17T05:00:00+10:00', stage:'Group I', group:'I', home:'France', away:'Senegal', venue:'New York/NJ'},
 {date:'2026-06-17T08:00:00+10:00', stage:'Group I', group:'I', home:'Iraq', away:'Norway', venue:'Boston'},
 {date:'2026-06-17T11:00:00+10:00', stage:'Group J', group:'J', home:'Argentina', away:'Algeria', venue:'Kansas City'},
 {date:'2026-06-17T14:00:00+10:00', stage:'Group J', group:'J', home:'Austria', away:'Jordan', venue:'San Francisco'},
 {date:'2026-06-18T03:00:00+10:00', stage:'Group K', group:'K', home:'Portugal', away:'Congo DR', venue:'Houston'},
 {date:'2026-06-18T06:00:00+10:00', stage:'Group L', group:'L', home:'England', away:'Croatia', venue:'Dallas'},
 {date:'2026-06-18T09:00:00+10:00', stage:'Group L', group:'L', home:'Ghana', away:'Panama', venue:'Toronto'},
 {date:'2026-06-18T12:00:00+10:00', stage:'Group K', group:'K', home:'Uzbekistan', away:'Colombia', venue:'Mexico City'},
 {date:'2026-06-19T02:00:00+10:00', stage:'Group A', group:'A', home:'Czechia', away:'South Africa', venue:'Atlanta'},
 {date:'2026-06-19T05:00:00+10:00', stage:'Group B', group:'B', home:'Switzerland', away:'Bosnia and Herzegovina', venue:'Los Angeles'},
 {date:'2026-06-19T08:00:00+10:00', stage:'Group B', group:'B', home:'Canada', away:'Qatar', venue:'Vancouver'},
 {date:'2026-06-19T11:00:00+10:00', stage:'Group A', group:'A', home:'Mexico', away:'South Korea', venue:'Guadalajara'},
 {date:'2026-06-20T05:00:00+10:00', stage:'Group D', group:'D', home:'USA', away:'Australia', venue:'Seattle'},
 {date:'2026-06-20T08:00:00+10:00', stage:'Group C', group:'C', home:'Scotland', away:'Morocco', venue:'Boston'},
 {date:'2026-06-20T11:00:00+10:00', stage:'Group C', group:'C', home:'Brazil', away:'Haiti', venue:'Philadelphia'},
 {date:'2026-06-20T14:00:00+10:00', stage:'Group D', group:'D', home:'Turkiye', away:'Paraguay', venue:'San Francisco'},
 {date:'2026-06-21T03:00:00+10:00', stage:'Group F', group:'F', home:'Netherlands', away:'Sweden', venue:'Houston'},
 {date:'2026-06-21T06:00:00+10:00', stage:'Group E', group:'E', home:'Germany', away:"Cote d'Ivoire", venue:'Toronto'},
 {date:'2026-06-21T10:00:00+10:00', stage:'Group E', group:'E', home:'Ecuador', away:'Curacao', venue:'Kansas City'},
 {date:'2026-06-21T14:00:00+10:00', stage:'Group F', group:'F', home:'Tunisia', away:'Japan', venue:'Monterrey'},
 {date:'2026-06-22T02:00:00+10:00', stage:'Group H', group:'H', home:'Spain', away:'Saudi Arabia', venue:'Atlanta'},
 {date:'2026-06-22T05:00:00+10:00', stage:'Group G', group:'G', home:'Belgium', away:'IR Iran', venue:'Los Angeles'},
 {date:'2026-06-22T08:00:00+10:00', stage:'Group H', group:'H', home:'Uruguay', away:'Cabo Verde', venue:'Miami'},
 {date:'2026-06-22T11:00:00+10:00', stage:'Group G', group:'G', home:'New Zealand', away:'Egypt', venue:'Vancouver'},
 {date:'2026-06-23T03:00:00+10:00', stage:'Group J', group:'J', home:'Argentina', away:'Austria', venue:'Dallas'},
 {date:'2026-06-23T07:00:00+10:00', stage:'Group I', group:'I', home:'France', away:'Iraq', venue:'Philadelphia'},
 {date:'2026-06-23T10:00:00+10:00', stage:'Group I', group:'I', home:'Norway', away:'Senegal', venue:'New York/NJ'},
 {date:'2026-06-23T13:00:00+10:00', stage:'Group J', group:'J', home:'Jordan', away:'Algeria', venue:'San Francisco'},
 {date:'2026-06-24T03:00:00+10:00', stage:'Group K', group:'K', home:'Portugal', away:'Uzbekistan', venue:'Houston'},
 {date:'2026-06-24T06:00:00+10:00', stage:'Group L', group:'L', home:'England', away:'Ghana', venue:'Boston'},
 {date:'2026-06-24T09:00:00+10:00', stage:'Group L', group:'L', home:'Panama', away:'Croatia', venue:'Toronto'},
 {date:'2026-06-24T12:00:00+10:00', stage:'Group K', group:'K', home:'Colombia', away:'Congo DR', venue:'Guadalajara'},
 {date:'2026-06-25T05:00:00+10:00', stage:'Group B', group:'B', home:'Switzerland', away:'Canada', venue:'Vancouver'},
 {date:'2026-06-25T05:00:00+10:00', stage:'Group B', group:'B', home:'Bosnia and Herzegovina', away:'Qatar', venue:'Seattle'},
 {date:'2026-06-25T08:00:00+10:00', stage:'Group C', group:'C', home:'Scotland', away:'Brazil', venue:'Miami'},
 {date:'2026-06-25T08:00:00+10:00', stage:'Group C', group:'C', home:'Morocco', away:'Haiti', venue:'Atlanta'},
 {date:'2026-06-25T11:00:00+10:00', stage:'Group A', group:'A', home:'Czechia', away:'Mexico', venue:'Mexico City'},
 {date:'2026-06-25T11:00:00+10:00', stage:'Group A', group:'A', home:'South Africa', away:'South Korea', venue:'Monterrey'},
 {date:'2026-06-26T06:00:00+10:00', stage:'Group E', group:'E', home:'Ecuador', away:'Germany', venue:'New York/NJ'},
 {date:'2026-06-26T06:00:00+10:00', stage:'Group E', group:'E', home:'Curacao', away:"Cote d'Ivoire", venue:'Philadelphia'},
 {date:'2026-06-26T09:00:00+10:00', stage:'Group F', group:'F', home:'Japan', away:'Sweden', venue:'Dallas'},
 {date:'2026-06-26T09:00:00+10:00', stage:'Group F', group:'F', home:'Tunisia', away:'Netherlands', venue:'Kansas City'},
 {date:'2026-06-26T12:00:00+10:00', stage:'Group D', group:'D', home:'Turkiye', away:'USA', venue:'Los Angeles'},
 {date:'2026-06-26T12:00:00+10:00', stage:'Group D', group:'D', home:'Paraguay', away:'Australia', venue:'San Francisco'}
];

let results = {};

async function loadResults() {
  const { data, error } = await supabase.from('scores').select('*');
  if (error) {
    console.error('Could not load scores:', error);
    return;
  }

  results = {};
  data.forEach(row => {
    results[row.match_id] = {
      h: row.home_score,
      a: row.away_score
    };
  });
}

async function saveResultToSupabase(matchId, homeScore, awayScore) {
  const { error } = await supabase.from('scores').upsert({
    match_id: String(matchId),
    home_score: Number(homeScore),
    away_score: Number(awayScore),
    updated_at: new Date().toISOString()
  });

  if (error) {
    console.error('Could not save score:', error);
    alert('Score could not be saved. Check Supabase settings.');
  }
}

function flag(team){ const c=codes[team]; if(!c)return '🏳️'; if(c.includes('-')) return c==='GB-ENG'?'🏴':c==='GB-SCT'?'🏴':'🏳️'; return c.replace(/./g,ch=>String.fromCodePoint(127397+ch.charCodeAt())); }
function owners(team){return people.filter(p=>p.teams.includes(team)).map(p=>p.name)}
function calcTeamPoints(){ const pts={}; Object.keys(codes).forEach(t=>pts[t]=0); fixtures.forEach((m,i)=>{const r=results[i]; if(!r||r.h===''||r.a===''||r.h===null||r.a===null)return; const h=+r.h,a=+r.a; if(h>a) pts[m.home]=(pts[m.home]||0)+3; else if(a>h) pts[m.away]=(pts[m.away]||0)+3; else {pts[m.home]=(pts[m.home]||0)+1; pts[m.away]=(pts[m.away]||0)+1;}}); return pts;}
function personStats(){ const pts=calcTeamPoints(); return people.map(p=>({ ...p, points:p.teams.reduce((s,t)=>s+(pts[t]||0),0), played:p.teams.reduce((s,t)=>s+fixtures.filter((m,i)=>(m.home===t||m.away===t)&&results[i]).length,0)})).sort((a,b)=>b.points-a.points||a.name.localeCompare(b.name));}
function avatar(name){ const img=localStorage.getItem('photo_'+name); return `<div class="avatar">${img?`<img src="${img}">`:name[0]}</div>`; }
function teamPill(t){return `<span class="pill">${flag(t)} ${t}</span>`}
function renderLeaderboard(){document.getElementById('leaderboardCards').innerHTML=personStats().map((p,i)=>`<article class="card"><div class="person-head"><span class="rank">#${i+1}</span>${avatar(p.name)}<div><h3>${p.name}</h3><div class="stats"><b>${p.points} pts</b><span>${p.played} results</span></div></div></div><div class="teams">${p.teams.map(teamPill).join('')}</div></article>`).join('')}
function renderIndividuals(){document.getElementById('individualCards').innerHTML=people.map(p=>`<article class="card"><div class="person-head">${avatar(p.name)}<div><h3>${p.name}</h3><label class="muted">Upload face photo <input type="file" accept="image/*" onchange="savePhoto(event,'${p.name}')"></label></div></div><div class="teams">${p.teams.map(teamPill).join('')}</div></article>`).join('')}
function renderTeams(q=''){ const rows=[]; people.forEach(p=>p.teams.forEach(t=>rows.push({team:t,person:p.name}))); document.getElementById('teamGrid').innerHTML=rows.filter(r=>(r.team+' '+r.person).toLowerCase().includes(q.toLowerCase())).sort((a,b)=>a.team.localeCompare(b.team)).map(r=>`<div class="team-row"><span>${flag(r.team)} <b>${r.team}</b></span><span class="owner">${r.person}</span></div>`).join('')}
function fmt(d){return new Intl.DateTimeFormat('en-AU',{timeZone:'Australia/Sydney',weekday:'short',day:'numeric',month:'short',hour:'numeric',minute:'2-digit',hour12:true,timeZoneName:'short'}).format(new Date(d))}
function renderSchedule(){ const now=new Date(); const upcoming=fixtures.find(m=>new Date(m.date)>now)||fixtures[0]; document.getElementById('nextMatch').textContent = `${flag(upcoming.home)} ${upcoming.home} v ${flag(upcoming.away)} ${upcoming.away} — ${fmt(upcoming.date)}`; document.getElementById('scheduleList').innerHTML=fixtures.map((m,i)=>{const r=results[i]; return `<div class="match"><div class="muted">${fmt(m.date)}</div><div><div class="match-teams">${flag(m.home)} ${m.home} v ${flag(m.away)} ${m.away} ${r?`<span class="owner">${r.h}-${r.a}</span>`:''}</div><div class="muted">${m.code ? m.code + ' · ' : ''}${m.stage || ('Group ' + m.group)} · ${m.venue}</div></div><div class="muted">${[...new Set([...owners(m.home),...owners(m.away)])].join(', ')}</div></div>`}).join('')}
function renderScores(){document.getElementById('scoreForms').innerHTML=fixtures.map((m,i)=>{const r=results[i]||{h:'',a:''}; return `<div class="score-card"><div><b>${flag(m.home)} ${m.home} v ${flag(m.away)} ${m.away}</b><br><span class="muted">${fmt(m.date)}</span></div><input type="number" min="0" value="${r.h}" data-i="${i}" data-side="h"><input type="number" min="0" value="${r.a}" data-i="${i}" data-side="a"><button onclick="saveScore(${i})">Save</button></div>`}).join('')}

async function saveScore(i){
  const inputs=[...document.querySelectorAll(`[data-i="${i}"]`)];
  const homeScore=inputs.find(x=>x.dataset.side==='h').value;
  const awayScore=inputs.find(x=>x.dataset.side==='a').value;

  results[i]={h:homeScore,a:awayScore};

  await saveResultToSupabase(i, homeScore, awayScore);
  renderAll();
}

function savePhoto(e,name){ const f=e.target.files[0]; if(!f)return; const reader=new FileReader(); reader.onload=()=>{localStorage.setItem('photo_'+name,reader.result); renderAll()}; reader.readAsDataURL(f); }
function renderAll(){renderLeaderboard(); renderIndividuals(); renderTeams(document.getElementById('teamSearch')?.value||''); renderSchedule(); renderScores();}

document.querySelectorAll('.tab').forEach(b=>b.onclick=()=>{document.querySelectorAll('.tab,.view').forEach(x=>x.classList.remove('active')); b.classList.add('active'); document.getElementById(b.dataset.view).classList.add('active')});
document.getElementById('teamSearch').oninput=e=>renderTeams(e.target.value);
document.getElementById('resetScores').onclick=async()=>{results={}; await supabase.from('scores').delete().neq('match_id',''); renderAll();};
document.getElementById('downloadSchedule').onclick=()=>{const csv='date_aest,stage,code,home,away,venue\n'+fixtures.map(m=>`"${fmt(m.date)}","${m.stage || ('Group '+m.group)}","${m.code||''}","${m.home}","${m.away}","${m.venue}"`).join('\n'); const a=document.createElement('a'); a.href=URL.createObjectURL(new Blob([csv],{type:'text/csv'})); a.download='world-cup-2026-aest-schedule.csv'; a.click();};
document.getElementById('fixtureImport').onchange=e=>{const f=e.target.files[0]; if(!f)return; const reader=new FileReader(); reader.onload=()=>{fixtures=JSON.parse(reader.result); localStorage.setItem('fixtures',JSON.stringify(fixtures)); renderAll()}; reader.readAsText(f);};

(async function init(){
  await loadResults();
  renderAll();
})();
