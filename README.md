<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
    <title>📱 Text Tales · Remote Friend Game</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }
        body {
            font-family: 'Segoe UI', Roboto, system-ui, -apple-system, sans-serif;
            background: #0f172a;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 16px;
            margin: 0;
        }
        .game-container {
            max-width: 480px;
            width: 100%;
            background: #1e293b;
            border-radius: 40px;
            padding: 24px 20px 32px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.6), 0 0 0 1px #334155;
            color: #f1f5f9;
            transition: all 0.2s;
        }
        h1 {
            font-size: 2rem;
            font-weight: 700;
            letter-spacing: -0.5px;
            display: flex;
            align-items: center;
            gap: 8px;
            margin-bottom: 6px;
        }
        .subhead {
            color: #94a3b8;
            font-size: 0.9rem;
            margin-bottom: 24px;
            border-left: 3px solid #facc15;
            padding-left: 12px;
        }
        .role-badge {
            display: inline-block;
            background: #2d3b52;
            padding: 6px 16px;
            border-radius: 40px;
            font-size: 0.8rem;
            font-weight: 600;
            color: #cbd5e1;
            letter-spacing: 0.3px;
            margin-bottom: 20px;
        }
        .card {
            background: #0f172a;
            border-radius: 28px;
            padding: 20px 18px;
            margin-bottom: 20px;
            border: 1px solid #334155;
        }
        .card-title {
            font-size: 0.75rem;
            text-transform: uppercase;
            letter-spacing: 1px;
            color: #64748b;
            margin-bottom: 12px;
        }
        .emoji-clue {
            font-size: 2.8rem;
            letter-spacing: 12px;
            background: #1e293b;
            padding: 12px 16px;
            border-radius: 60px;
            display: inline-block;
            border: 1px dashed #475569;
        }
        .flex-row {
            display: flex;
            flex-wrap: wrap;
            align-items: center;
            gap: 10px;
            margin: 12px 0 6px;
        }
        .word-badge {
            background: #2d3b52;
            border-radius: 40px;
            padding: 8px 18px;
            font-size: 1.2rem;
            font-weight: 500;
        }
        .label-sm {
            font-size: 0.7rem;
            color: #94a3b8;
            letter-spacing: 0.5px;
        }
        input, textarea {
            width: 100%;
            padding: 14px 16px;
            background: #0f172a;
            border: 1px solid #334155;
            border-radius: 60px;
            color: #f1f5f9;
            font-size: 1rem;
            outline: none;
            transition: 0.2s;
            margin: 6px 0 10px;
        }
        input:focus, textarea:focus {
            border-color: #facc15;
            box-shadow: 0 0 0 3px rgba(250, 204, 21, 0.15);
        }
        textarea {
            border-radius: 24px;
            resize: vertical;
            min-height: 70px;
            font-family: inherit;
        }
        .btn-group {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
            margin: 12px 0 8px;
        }
        .btn {
            background: #334155;
            border: none;
            padding: 12px 22px;
            border-radius: 60px;
            font-weight: 600;
            font-size: 0.95rem;
            color: #f1f5f9;
            cursor: pointer;
            transition: 0.15s;
            flex: 1 0 auto;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: 6px;
            border: 1px solid transparent;
        }
        .btn-primary {
            background: #facc15;
            color: #0f172a;
            border-color: #facc15;
        }
        .btn-primary:hover {
            background: #fde047;
            transform: scale(0.97);
        }
        .btn-outline {
            background: transparent;
            border: 1px solid #475569;
        }
        .btn-outline:hover {
            background: #2d3b52;
        }
        .btn-danger {
            background: #b91c1c;
            color: white;
        }
        .btn-success {
            background: #15803d;
            color: white;
        }
        .btn-whatsapp {
            background: #25d366;
            color: white;
            border-color: #25d366;
        }
        .btn-whatsapp:hover {
            background: #20b858;
            transform: scale(0.97);
        }
        .btn:active { transform: scale(0.95); }
        .btn:disabled { opacity: 0.4; pointer-events: none; }

        .chat-box {
            background: #0f172a;
            border-radius: 24px;
            padding: 12px 14px;
            max-height: 220px;
            overflow-y: auto;
            border: 1px solid #2d3b52;
            margin: 12px 0 10px;
            font-size: 0.95rem;
            line-height: 1.6;
        }
        .chat-msg {
            padding: 6px 0;
            border-bottom: 1px solid #1e293b;
        }
        .chat-msg:last-child { border-bottom: none; }
        .msg-keeper { color: #facc15; }
        .msg-sleuth { color: #7dd3fc; }
        .msg-system { color: #94a3b8; font-style: italic; font-size: 0.85rem; }

        .status-box {
            background: #1e293b;
            padding: 12px 16px;
            border-radius: 60px;
            font-size: 0.9rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-top: 10px;
            border: 1px solid #334155;
        }
        .counter {
            background: #2d3b52;
            padding: 4px 16px;
            border-radius: 40px;
            font-weight: 700;
            font-size: 1.2rem;
        }
        .footer-note {
            color: #64748b;
            font-size: 0.7rem;
            text-align: center;
            margin-top: 24px;
            border-top: 1px solid #2d3b52;
            padding-top: 18px;
        }
        .inline-flex { display: inline-flex; align-items: center; gap: 6px; }
        .mt-8 { margin-top: 8px; }
        .mb-8 { margin-bottom: 8px; }
        .gap-4 { gap: 4px; }
        .flex-wrap { flex-wrap: wrap; }
        .w-full { width: 100%; }
        .text-center { text-align: center; }

        /* scroll */
        .chat-box::-webkit-scrollbar { width: 4px; }
        .chat-box::-webkit-scrollbar-track { background: #0f172a; }
        .chat-box::-webkit-scrollbar-thumb { background: #475569; border-radius: 10px; }

        /* Share notification */
        .share-notification {
            background: #15803d;
            color: white;
            padding: 10px 16px;
            border-radius: 60px;
            font-size: 0.85rem;
            margin-top: 8px;
            display: none;
            animation: fadeIn 0.3s ease;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(-10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .share-box {
            background: #0f172a;
            border: 1px solid #334155;
            border-radius: 16px;
            padding: 12px 14px;
            margin-top: 8px;
            font-size: 0.75rem;
            color: #94a3b8;
            word-break: break-all;
            display: none;
        }
        .share-box.show {
            display: block;
        }
        .share-box a {
            color: #facc15;
            text-decoration: none;
        }
    </style>
</head>
<body>
<div class="game-container" id="app">
    <h1>📖 Text Tales</h1>
    <div class="subhead">🎯 5‑question story heist · remote play</div>

    <!-- Role & status -->
    <div class="flex-row" style="justify-content:space-between;">
        <span class="role-badge" id="roleDisplay">🔮 Keeper</span>
        <span class="role-badge" id="turnIndicator">⏳ Sleuth's turn</span>
    </div>

    <!-- SECRET (Keeper) -->
    <div class="card" id="keeperSection">
        <div class="card-title">🔐 KEEPER · set your secret</div>
        <div class="flex-row flex-wrap">
            <span class="label-sm">Character</span>
            <input type="text" id="charInput" placeholder="e.g. pirate" value="pirate" />
        </div>
        <div class="flex-row flex-wrap">
            <span class="label-sm">Object</span>
            <input type="text" id="objInput" placeholder="e.g. compass" value="compass" />
        </div>
        <div class="flex-row flex-wrap">
            <span class="label-sm">Location</span>
            <input type="text" id="locInput" placeholder="e.g. library" value="library" />
        </div>
        <div class="btn-group">
            <button class="btn btn-primary" id="setSecretBtn">✨ Set secret &amp; show clues</button>
        </div>
        <div id="clueDisplay" class="mt-8" style="display:flex; align-items:center; gap:12px; flex-wrap:wrap;">
            <span class="label-sm">🔎 Clues (3 emojis):</span>
            <span class="emoji-clue" id="emojiClue">🏴‍☠️ 🧭 📚</span>
        </div>
        <div class="flex-row" style="margin-top:6px;">
            <span class="label-sm">📤 Share these clues with the Sleuth</span>
        </div>
    </div>

    <!-- Sleuth's question & answer -->
    <div class="card" id="sleuthSection">
        <div class="card-title">🔍 SLEUTH · ask a yes/no question</div>
        <input type="text" id="questionInput" placeholder='e.g. "Is the object metal?"' />
        <div class="btn-group">
            <button class="btn btn-primary" id="askBtn">❓ Ask question</button>
            <button class="btn btn-outline" id="guessBtn">🎯 Make final guess</button>
        </div>
        <div class="flex-row" style="margin-top:4px;">
            <span class="label-sm">Keeper's answer (1 word + 1 emoji):</span>
            <span class="word-badge" id="keeperAnswerDisplay">—</span>
        </div>
        <div class="flex-row" style="justify-content:space-between;">
            <span class="label-sm">Questions left: <span id="questionsLeft">5</span></span>
            <span class="label-sm">Status: <span id="gameStatus">⏳ playing</span></span>
        </div>
    </div>

    <!-- Guess panel (popup style) -->
    <div class="card" id="guessPanel" style="display:none; background:#1e293b; border-color:#facc15;">
        <div class="card-title">🎯 FINAL GUESS</div>
        <div class="flex-row flex-wrap">
            <span class="label-sm">Character</span>
            <input type="text" id="guessChar" placeholder="character" />
        </div>
        <div class="flex-row flex-wrap">
            <span class="label-sm">Object</span>
            <input type="text" id="guessObj" placeholder="object" />
        </div>
        <div class="flex-row flex-wrap">
            <span class="label-sm">Location</span>
            <input type="text" id="guessLoc" placeholder="location" />
        </div>
        <button class="btn btn-success" id="submitGuessBtn">✅ Submit guess</button>
        <button class="btn btn-outline" id="cancelGuessBtn" style="margin-top:6px;">Cancel</button>
    </div>

    <!-- Chat / log -->
    <div class="card" style="padding-bottom:12px;">
        <div class="card-title">📜 game log</div>
        <div class="chat-box" id="chatLog">
            <div class="chat-msg msg-system">🤝 Set a secret (Keeper) and share clues to start.</div>
        </div>
    </div>

    <!-- status & controls -->
    <div class="status-box">
        <span id="statusText">⚡ Ready</span>
        <span class="counter" id="roundCounter">0/5</span>
    </div>
    <div class="btn-group" style="margin-top:8px;">
        <button class="btn btn-outline" id="resetBtn">🔄 New round</button>
        <button class="btn btn-outline" id="switchRoleBtn">🔄 Switch roles</button>
        <button class="btn btn-whatsapp" id="shareBtn">📲 Share via WhatsApp</button>
    </div>

    <!-- Share section -->
    <div id="shareSection" class="share-box">
        <p style="margin-bottom:6px;">📋 Share this link with your friend:</p>
        <input type="text" id="shareLinkInput" readonly style="font-size:0.7rem; padding:8px 12px; margin:4px 0;" />
        <div class="btn-group" style="margin-top:4px;">
            <button class="btn btn-outline" id="copyLinkBtn" style="flex:0 1 auto; padding:6px 16px; font-size:0.8rem;">📋 Copy</button>
            <button class="btn btn-whatsapp" id="whatsappShareBtn" style="flex:0 1 auto; padding:6px 16px; font-size:0.8rem;">💬 Send</button>
        </div>
        <div id="copyNotification" class="share-notification" style="display:none;">✅ Copied to clipboard!</div>
    </div>

    <div class="footer-note">
        📱 One device? Pass the phone · or share the link above to play remotely.
    </div>
</div>
<script>
    (function(){
        "use strict";

        // ----- DOM refs -----
        const charInput = document.getElementById('charInput');
        const objInput = document.getElementById('objInput');
        const locInput = document.getElementById('locInput');
        const setSecretBtn = document.getElementById('setSecretBtn');
        const emojiClue = document.getElementById('emojiClue');

        const questionInput = document.getElementById('questionInput');
        const askBtn = document.getElementById('askBtn');
        const guessBtn = document.getElementById('guessBtn');
        const keeperAnswerDisplay = document.getElementById('keeperAnswerDisplay');
        const questionsLeftSpan = document.getElementById('questionsLeft');
        const gameStatusSpan = document.getElementById('gameStatus');
        const chatLog = document.getElementById('chatLog');
        const statusText = document.getElementById('statusText');
        const roundCounter = document.getElementById('roundCounter');

        const guessPanel = document.getElementById('guessPanel');
        const guessChar = document.getElementById('guessChar');
        const guessObj = document.getElementById('guessObj');
        const guessLoc = document.getElementById('guessLoc');
        const submitGuessBtn = document.getElementById('submitGuessBtn');
        const cancelGuessBtn = document.getElementById('cancelGuessBtn');

        const resetBtn = document.getElementById('resetBtn');
        const switchRoleBtn = document.getElementById('switchRoleBtn');
        const shareBtn = document.getElementById('shareBtn');
        const shareSection = document.getElementById('shareSection');
        const shareLinkInput = document.getElementById('shareLinkInput');
        const copyLinkBtn = document.getElementById('copyLinkBtn');
        const whatsappShareBtn = document.getElementById('whatsappShareBtn');
        const copyNotification = document.getElementById('copyNotification');

        const roleDisplay = document.getElementById('roleDisplay');
        const turnIndicator = document.getElementById('turnIndicator');

        // ----- state -----
        let secret = { character: 'pirate', object: 'compass', location: 'library' };
        let questionsUsed = 0;
        const MAX_QUESTIONS = 5;
        let gameActive = true;
        let role = 'keeper';
        let turn = 'sleuth';

        // ----- FULL EMOJI MAP (100+ emojis) -----
        function getEmojiForWord(word) {
            const map = {
                // ---- CHARACTERS ----
                'pirate': '🏴‍☠️', 'knight': '🛡️', 'wizard': '🧙', 'detective': '🕵️',
                'chef': '👨‍🍳', 'astronaut': '👨‍🚀', 'artist': '🎨', 'sailor': '⛵',
                'ninja': '🥷', 'vampire': '🧛', 'zombie': '🧟', 'ghost': '👻',
                'alien': '👽', 'robot': '🤖', 'clown': '🤡', 'joker': '🃏',
                'king': '👑', 'queen': '👑', 'prince': '🤴', 'princess': '👸',
                'superhero': '🦸', 'supervillain': '🦹', 'elf': '🧝', 'fairy': '🧚',
                'mermaid': '🧜', 'genie': '🧞', 'angel': '👼', 'devil': '👿',
                'student': '👩‍🎓', 'teacher': '👨‍🏫', 'doctor': '👨‍⚕️', 'nurse': '👩‍⚕️',
                'police': '👮', 'firefighter': '🧑‍🚒', 'soldier': '🪖', 'farmer': '👨‍🌾',
                'worker': '👷', 'scientist': '👨‍🔬', 'pilot': '🧑‍✈️', 'judge': '⚖️',
                'lawyer': '⚖️', 'cowboy': '🤠', 'explorer': '🧭', 'hunter': '🏹',
                'mage': '🧙', 'druid': '🌿', 'bard': '🎵', 'ranger': '🏹',
                'monk': '🧘', 'samurai': '⚔️', 'viking': '🪓', 'gladiator': '⚔️',
                'spy': '🕵️', 'thief': '🥷', 'assassin': '🗡️', 'bodyguard': '🛡️',
                'agent': '🎯', 'reporter': '📰', 'photographer': '📸', 'musician': '🎵',
                'dancer': '💃', 'actor': '🎭', 'director': '🎬', 'writer': '✍️',
                'poet': '📝', 'philosopher': '🧠', 'inventor': '💡', 'engineer': '⚙️',
                'architect': '🏛️', 'captain': '🚢', 'commander': '🎖️', 'president': '🏛️',
                'mayor': '🏛️', 'citizen': '🧑', 'child': '👦', 'baby': '👶',
                'teenager': '🧑', 'adult': '🧑', 'elder': '👴', 'grandma': '👵',
                'grandpa': '👴', 'friend': '🤝', 'enemy': '👿', 'hero': '🦸',
                'villain': '🦹', 'monster': '👹', 'dragon': '🐉', 'unicorn': '🦄',
                'phoenix': '🔥', 'goblin': '👺', 'orc': '👹', 'troll': '🧌',
                'giant': '🗿', 'dwarf': '⛏️', 'gnome': '🍄', 'centaur': '🐴',
                'sphinx': '🦁', 'griffin': '🦅', 'manticore': '🦁', 'basilisk': '🐍',
                'chimera': '🦁', 'kraken': '🐙', 'leviathan': '🐋', 'serpent': '🐍',

                // ---- OBJECTS ----
                'compass': '🧭', 'sword': '⚔️', 'wand': '🪄', 'knife': '🔪',
                'brush': '🖌️', 'anchor': '⚓', 'map': '🗺️', 'book': '📚',
                'scroll': '📜', 'potion': '🧪', 'crystal': '💎', 'gem': '💎',
                'diamond': '💎', 'gold': '🪙', 'silver': '🪙', 'coin': '🪙',
                'key': '🔑', 'lock': '🔒', 'shield': '🛡️', 'armor': '🛡️',
                'helmet': '⛑️', 'crown': '👑', 'ring': '💍', 'necklace': '📿',
                'bracelet': '📿', 'staff': '🪄', 'dagger': '🗡️', 'axe': '🪓',
                'hammer': '🔨', 'spear': '🔱', 'bow': '🏹', 'arrow': '🏹',
                'gun': '🔫', 'bomb': '💣', 'rocket': '🚀', 'satellite': '🛰️',
                'telescope': '🔭', 'microscope': '🔬', 'test tube': '🧪', 'beaker': '🧪',
                'bottle': '🍾', 'cup': '🥤', 'glass': '🥃', 'plate': '🍽️',
                'bowl': '🥣', 'spoon': '🥄', 'fork': '🍴', 'pot': '🍲',
                'pan': '🍳', 'lamp': '🪔', 'candle': '🕯️', 'torch': '🔥',
                'battery': '🔋', 'radio': '📻', 'camera': '📷', 'phone': '📱',
                'computer': '💻', 'tablet': '📱', 'watch': '⌚', 'clock': '🕰️',
                'umbrella': '☂️', 'bag': '👜', 'suitcase': '🧳', 'box': '📦',
                'chest': '📦', 'treasure': '💰', 'money': '💰', 'bill': '💵',
                'card': '🃏', 'ticket': '🎫', 'letter': '✉️', 'pen': '🖊️',
                'pencil': '✏️', 'eraser': '🧹', 'ruler': '📏', 'scissors': '✂️',
                'needle': '🪡', 'thread': '🧵', 'rope': '🪢', 'chain': '⛓️',
                'ladder': '🪜', 'bucket': '🪣', 'broom': '🧹', 'mop': '🧹',
                'soap': '🧼', 'sponge': '🧽', 'towel': '🧻', 'blanket': '🛏️',
                'pillow': '🛏️', 'bed': '🛏️', 'chair': '🪑', 'table': '🪑',
                'door': '🚪', 'window': '🪟', 'mirror': '🪞', 'statue': '🗿',
                'painting': '🖼️', 'photo': '🖼️', 'trophy': '🏆', 'medal': '🎖️',
                'badge': '🎖️',

                // ---- LOCATIONS ----
                'library': '📚', 'castle': '🏰', 'forest': '🌲', 'museum': '🏛️',
                'kitchen': '🍳', 'moon': '🌕', 'island': '🏝️', 'beach': '🏖️',
                'mountain': '🏔️', 'city': '🏙️', 'village': '🏘️', 'house': '🏠',
                'home': '🏠', 'cave': '🕳️', 'dungeon': '🕳️', 'tower': '🗼',
                'palace': '🏛️', 'temple': '🛕', 'church': '⛪', 'mosque': '🕌',
                'synagogue': '🕍', 'school': '🏫', 'university': '🏫', 'college': '🏫',
                'hospital': '🏥', 'clinic': '🏥', 'bank': '🏦', 'market': '🏪',
                'shop': '🏪', 'restaurant': '🍽️', 'cafe': '☕', 'hotel': '🏨',
                'motel': '🏨', 'airport': '✈️', 'train station': '🚉', 'bus stop': '🚏',
                'harbor': '⚓', 'port': '⚓', 'lighthouse': '🗼', 'desert': '🏜️',
                'jungle': '🌴', 'ocean': '🌊', 'sea': '🌊', 'lake': '🏞️',
                'river': '🌊', 'waterfall': '🌊', 'volcano': '🌋', 'space': '🚀',
                'starship': '🛸', 'planet': '🪐', 'galaxy': '🌌', 'laboratory': '🔬',
                'office': '🏢', 'factory': '🏭', 'warehouse': '🏚️', 'mansion': '🏚️',
                'cottage': '🏡', 'cabin': '🏡', 'tent': '⛺', 'camp': '⛺',
                'garden': '🌻', 'park': '🌳', 'zoo': '🦁', 'aquarium': '🐠',
                'stadium': '🏟️', 'arena': '🏟️', 'theater': '🎭', 'cinema': '🎬',
                'studio': '🎬', 'courtroom': '⚖️'
            };

            const lower = word.toLowerCase().trim();
            if (map[lower]) return map[lower];
            if (lower.includes('man') || lower.includes('woman') || lower.includes('person') || lower.includes('human')) return '🧑';
            if (lower.includes('animal') || lower.includes('creature') || lower.includes('beast')) return '🐾';
            if (lower.includes('place') || lower.includes('land') || lower.includes('area')) return '📍';
            if (lower.includes('thing') || lower.includes('item') || lower.includes('object')) return '📦';
            return '❓';
        }

        function generateClueEmojis(secretObj) {
            const c = getEmojiForWord(secretObj.character) || '👤';
            const o = getEmojiForWord(secretObj.object) || '📦';
            const l = getEmojiForWord(secretObj.location) || '📍';
            return `${c} ${o} ${l}`;
        }

        function updateClueDisplay() {
            emojiClue.textContent = generateClueEmojis(secret);
        }

        function addChat(msg, type = 'system') {
            const div = document.createElement('div');
            div.className = `chat-msg msg-${type}`;
            div.textContent = msg;
            chatLog.appendChild(div);
            chatLog.scrollTop = chatLog.scrollHeight;
        }

        function updateUI() {
            questionsLeftSpan.textContent = MAX_QUESTIONS - questionsUsed;
            roundCounter.textContent = `${questionsUsed}/${MAX_QUESTIONS}`;
            if (questionsUsed >= MAX_QUESTIONS && gameActive) {
                gameActive = false;
                gameStatusSpan.textContent = '❌ out of questions';
                statusText.textContent = '⏳ Sleuth lost – reveal secret?';
                addChat('❌ No more questions! Keeper wins. (Click "New round" to replay)', 'system');
                turnIndicator.textContent = '🏁 game over';
                return;
            }
            if (gameActive) {
                gameStatusSpan.textContent = '⏳ playing';
                statusText.textContent = turn === 'sleuth' ? '🤔 Sleuth turn' : '👀 Keeper answers';
                turnIndicator.textContent = turn === 'sleuth' ? '🔍 Sleuth asks' : '🔮 Keeper replies';
            } else {
                turnIndicator.textContent = '🏁 game over';
            }
            roleDisplay.textContent = role === 'keeper' ? '🔮 Keeper' : '🕵️ Sleuth';
        }

        function resetGame(newSecret = null) {
            if (newSecret) {
                secret = newSecret;
                charInput.value = secret.character;
                objInput.value = secret.object;
                locInput.value = secret.location;
                updateClueDisplay();
            }
            questionsUsed = 0;
            gameActive = true;
            turn = 'sleuth';
            keeperAnswerDisplay.textContent = '—';
            questionInput.value = '';
            guessPanel.style.display = 'none';
            chatLog.innerHTML = '';
            addChat('🔄 New round started! Keeper sets secret, share clues.', 'system');
            addChat(`🔎 Clues: ${generateClueEmojis(secret)}`, 'system');
            updateUI();
            guessChar.value = '';
            guessObj.value = '';
            guessLoc.value = '';
        }

        function setSecret() {
            const c = charInput.value.trim() || 'pirate';
            const o = objInput.value.trim() || 'compass';
            const l = locInput.value.trim() || 'library';
            secret = { character: c, object: o, location: l };
            updateClueDisplay();
            addChat(`🔐 Keeper set new secret. Clues: ${generateClueEmojis(secret)}`, 'system');
            if (!gameActive) {
                gameActive = true;
                questionsUsed = 0;
                addChat('🔄 Secret updated – game is active again.', 'system');
            } else {
                questionsUsed = 0;
                addChat('🔄 Secret changed – questions reset to 0.', 'system');
            }
            turn = 'sleuth';
            keeperAnswerDisplay.textContent = '—';
            updateUI();
            guessPanel.style.display = 'none';
        }

        function askQuestion() {
            if (!gameActive) {
                addChat('⛔ Game over. Start a new round.', 'system');
                return;
            }
            if (role === 'keeper') {
                addChat('⛔ You are the Keeper – pass the phone or switch roles.', 'system');
                return;
            }
            if (turn !== 'sleuth') {
                addChat('⏳ Wait for the Keeper to answer first.', 'system');
                return;
            }
            if (questionsUsed >= MAX_QUESTIONS) {
                addChat('⛔ No questions left!', 'system');
                return;
            }
            const q = questionInput.value.trim();
            if (!q) {
                addChat('✏️ Type a yes/no question.', 'system');
                return;
            }
            questionsUsed++;
            addChat(`❓ Sleuth: "${q}"`, 'sleuth');
            questionInput.value = '';

            const answers = [
                { word: 'Maybe', emoji: '🤔' }, { word: 'Likely', emoji: '👍' },
                { word: 'Unlikely', emoji: '👎' }, { word: 'Usually', emoji: '⏳' },
                { word: 'Rarely', emoji: '❄️' }, { word: 'Yes', emoji: '✅' },
                { word: 'No', emoji: '🚫' }, { word: 'Sorta', emoji: '🌓' },
                { word: 'Definitely', emoji: '🔥' }, { word: 'Never', emoji: '🚷' },
            ];
            const idx = Math.floor(Math.random() * answers.length);
            const ans = answers[idx];
            const reply = `${ans.word} ${ans.emoji}`;
            keeperAnswerDisplay.textContent = reply;
            addChat(`🔮 Keeper: "${reply}"`, 'keeper');

            turn = 'sleuth';
            updateUI();

            if (questionsUsed >= MAX_QUESTIONS) {
                gameActive = false;
                addChat('⏳ Out of questions! Click "New round" or make a guess if you haven\'t.', 'system');
                updateUI();
            }
            guessPanel.style.display = 'none';
        }

        function showGuessPanel() {
            if (role === 'keeper') {
                addChat('⛔ Switch to Sleuth role to guess.', 'system');
                return;
            }
            guessPanel.style.display = 'block';
            guessChar.value = '';
            guessObj.value = '';
            guessLoc.value = '';
        }

        function submitGuess() {
            const gc = guessChar.value.trim().toLowerCase();
            const go = guessObj.value.trim().toLowerCase();
            const gl = guessLoc.value.trim().toLowerCase();
            if (!gc || !go || !gl) {
                addChat('✏️ Fill in all three fields for your guess.', 'system');
                return;
            }
            const sChar = secret.character.toLowerCase();
            const sObj = secret.object.toLowerCase();
            const sLoc = secret.location.toLowerCase();
            const exact = (gc === sChar && go === sObj && gl === sLoc);
            if (exact) {
                addChat(`🎉🎉🎉 SLEUTH WINS! Exact guess: "${gc}, ${go}, ${gl}"`, 'system');
                gameActive = false;
                gameStatusSpan.textContent = '🏆 Sleuth wins!';
                statusText.textContent = '🎉 Correct!';
                turnIndicator.textContent = '🏆 Sleuth wins!';
            } else {
                addChat(`❌ Wrong guess. Keeper wins this round. Secret was: "${secret.character}, ${secret.object}, ${secret.location}"`, 'system');
                gameActive = false;
                gameStatusSpan.textContent = '🏆 Keeper wins!';
                statusText.textContent = '❌ Incorrect guess';
                turnIndicator.textContent = '🏆 Keeper wins!';
            }
            guessPanel.style.display = 'none';
            updateUI();
        }

        function cancelGuess() {
            guessPanel.style.display = 'none';
        }

        function switchRoles() {
            role = (role === 'keeper') ? 'sleuth' : 'keeper';
            roleDisplay.textContent = role === 'keeper' ? '🔮 Keeper' : '🕵️ Sleuth';
            addChat(`🔄 Switched roles: now you are the ${role}.`, 'system');
            turn = 'sleuth';
            updateUI();
            guessPanel.style.display = 'none';
        }

        function fullReset() {
            resetGame(secret);
            guessPanel.style.display = 'none';
            addChat('🔄 Full reset – same secret.', 'system');
        }

        // ----- SHARE FUNCTIONS -----
        function getShareLink() {
            // Use the current page URL or a fallback
            const url = window.location.href;
            return url;
        }

        function toggleShareSection() {
            const isVisible = shareSection.classList.contains('show');
            if (isVisible) {
                shareSection.classList.remove('show');
                shareSection.style.display = 'none';
            } else {
                shareSection.style.display = 'block';
                // Force reflow then add class for animation
                void shareSection.offsetWidth;
                shareSection.classList.add('show');
                const link = getShareLink();
                shareLinkInput.value = link;
            }
        }

        function copyShareLink() {
            const link = shareLinkInput.value;
            if (navigator.clipboard && navigator.clipboard.writeText) {
                navigator.clipboard.writeText(link).then(() => {
                    showCopyNotification();
                }).catch(() => {
                    fallbackCopy(link);
                });
            } else {
                fallbackCopy(link);
            }
        }

        function fallbackCopy(text) {
            shareLinkInput.select();
            shareLinkInput.setSelectionRange(0, 99999);
            try {
                document.execCommand('copy');
                showCopyNotification();
            } catch (err) {
                alert('Copy failed. Please copy the link manually.');
            }
        }

        function showCopyNotification() {
            copyNotification.style.display = 'block';
            setTimeout(() => {
                copyNotification.style.display = 'none';
            }, 3000);
        }

        function shareViaWhatsApp() {
            const link = getShareLink();
            const message = encodeURIComponent(
                `🎮 Let's play Text Tales!\n\n` +
                `Here's the game link:\n${link}\n\n` +
                `🔎 One of us is the Keeper (sets a secret), the other is the Sleuth (asks 5 yes/no questions to guess).\n` +
                `📱 Open the link and let's play!`
            );
            const whatsappUrl = `https://wa.me/?text=${message}`;
            window.open(whatsappUrl, '_blank');
        }

        // ----- event binding -----
        setSecretBtn.addEventListener('click', setSecret);
        askBtn.addEventListener('click', askQuestion);
        guessBtn.addEventListener('click', showGuessPanel);
        submitGuessBtn.addEventListener('click', submitGuess);
        cancelGuessBtn.addEventListener('click', cancelGuess);
        resetBtn.addEventListener('click', fullReset);
        switchRoleBtn.addEventListener('click', switchRoles);
        shareBtn.addEventListener('click', toggleShareSection);
        copyLinkBtn.addEventListener('click', copyShareLink);
        whatsappShareBtn.addEventListener('click', shareViaWhatsApp);

        questionInput.addEventListener('keypress', (e) => {
            if (e.key === 'Enter') askBtn.click();
        });

        // init
        (function init() {
            secret = {
                character: charInput.value.trim() || 'pirate',
                object: objInput.value.trim() || 'compass',
                location: locInput.value.trim() || 'library'
            };
            updateClueDisplay();
            resetGame(secret);
            role = 'keeper';
            roleDisplay.textContent = '🔮 Keeper';
            turn = 'sleuth';
            updateUI();
            addChat('📱 Both players can share this page. Keeper sets secret, shares clues, Sleuth asks 5 questions.', 'system');
        })();

    })();
</script>
</body>
</html>
