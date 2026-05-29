import { app } from "./firebase-config.js";

import {
    getFirestore,
    collection,
    addDoc,
    setDoc,
    getDoc,        // 🔥 AJOUT IMPORTANT
    getDocs,
    deleteDoc,
    doc
}

 from "https://www.gstatic.com/firebasejs/10.12.2/firebase-firestore.js";

const db = getFirestore(app);




import {
    getAuth,
    createUserWithEmailAndPassword,
    signInWithEmailAndPassword,
    signOut,
    sendPasswordResetEmail
}
from "https://www.gstatic.com/firebasejs/10.12.2/firebase-auth.js";

const auth = getAuth(app);




window.addEventListener("DOMContentLoaded", () => {

    const authModal = document.getElementById("authModal");

    const openLoginBtn = document.getElementById("openLoginBtn");
    const openRegisterBtn = document.getElementById("openRegisterBtn");
    const closeAuthBtn = document.getElementById("closeAuthBtn");

    const loginForm = document.getElementById("loginForm");
    const registerForm = document.getElementById("registerForm");
    const forgotForm = document.getElementById("forgotForm");

    let currentMode = "login";

    function showModal(mode) {

        if (!authModal) return;

        authModal.classList.remove("hidden");

        loginForm?.classList.add("hidden");
        registerForm?.classList.add("hidden");
        forgotForm?.classList.add("hidden");

        if (mode === "login") loginForm?.classList.remove("hidden");
        if (mode === "register") registerForm?.classList.remove("hidden");
        if (mode === "forgot") forgotForm?.classList.remove("hidden");

        currentMode = mode;
        updateModalHeader();
    }
    
    
    document.getElementById("forgotForm")?.addEventListener("submit", async (e) => {
    e.preventDefault();

    const email = document
        .getElementById("forgotForm")
        .querySelector('input[type="email"]')?.value;

    if (!email) return;

    try {
        await sendPasswordResetEmail(auth, email);

        alert("Un email de réinitialisation a été envoyé !");

        showModal("login");

    } catch (error) {
        alert("Erreur: " + error.message);
    }
});
    
    
    
    
    
    
    
    
    
   document.getElementById("joinFamilyBtn")?.addEventListener("click", async () => {
    const code = prompt("Entrez le code familial fourni par le membre principal :");
    if (!code) return;

    try {
        // 🔹 Chercher l'utilisateur principal correspondant au code
        const usersSnap = await getDocs(collection(db, "users"));
        const mainUser = usersSnap.docs.find(d => d.data().familyCode === code);

        if (!mainUser) {
            alert("Code invalide !");
            return;
        }

        // 🔹 Créer un compte lié à cette famille
        const pseudoEmail = `fam_${Date.now()}@temp.com`;
        const pseudoPass = generateFamilyCode(); // mot de passe aléatoire
        const userCredential = await createUserWithEmailAndPassword(auth, pseudoEmail, pseudoPass);
        const user = userCredential.user;

        // 🔹 Sauvegarder cet utilisateur lié avec le même code familial
        await setDoc(doc(db, "users", user.uid), {
    uid: user.uid, // 🔥 AJOUT IMPORTANT
            email: pseudoEmail,
            familyCode: code,
            createdAt: Date.now()
        });

        alert("Vous avez rejoint la famille avec succès !");
        loginSuccess();

    } catch (error) {
        alert("Erreur : " + error.message);
    }
}); 
    
    
    
    
    

    function closeModal() {
        authModal?.classList.add("hidden");
    }

    openLoginBtn?.addEventListener("click", () => showModal("login"));
    openRegisterBtn?.addEventListener("click", () => showModal("register"));
    
    
    document.getElementById("openForgotBtn")
?.addEventListener("click", () => {
    showModal("forgot");
});



document.getElementById("openRegisterBtn2")
?.addEventListener("click", () => {
    showModal("register");
});

    closeAuthBtn?.addEventListener("click", closeModal);

    const baseText = {
        fr: {
            hero_title: "Bienvenue sur MicroNest",
            hero_subtitle: "Gérez votre maison facilement et sans stress",
            btn_register: "Créer un compte",
            btn_login: "Se connecter",
search_placeholder: "Rechercher un objet...",
            login_title: "Connexion",
            login_message: "Entrez vos identifiants pour continuer",
            register_title: "Créer un compte",
            register_message: "Rejoignez-nous pour gérer votre maison",
            forgot_title: "Mot de passe oublié",
            forgot_instructions: "Entrez votre email pour réinitialiser votre mot de passe.",

            label_email: "Email",
            label_password: "Mot de passe",

            link_forgot: "Mot de passe oublié ?",
            btn_connect: "Se connecter",

            text_no_account: "Pas encore de compte ?",
            link_register: "Créer un compte",
            text_have_account: "Déjà inscrit ?",
            link_login: "Se connecter",
            btn_delete: "Supprimer",

            btn_register_submit: "Créer mon compte",
            btn_forgot_submit: "Envoyer le lien",
            link_back_login: "Retour à la connexion",

            p2_title: "Votre Tableau de Bord Familial",
            p2_subtitle: "Organisez votre maison simplement",

            menu_find: "Trouver un objet",
            menu_reminders: "Rappels",
            menu_messages: "Messages",

            title_find: "Où est mon objet ?",
            title_reminders: "Rappels & Maintenance",
            title_messages: "Notes pour la famille",

            btn_back: "➔ Retour",

            obj_name: "Ex: Passeport",
            obj_loc: "Ex: Tiroir",

            rem_text: "Ex: Changer filtre",
            rem_days: "Jours",

            msg_placeholder: "Ex: Message important..."
        },

        en: {
            hero_title: "Welcome to MicroNest",
            hero_subtitle: "Manage your home easily and stress-free",
            btn_register: "Sign Up",
            btn_login: "Log In",

            login_title: "Login",
            login_message: "Enter your credentials to continue",
            search_placeholder: "Search an object...",
            register_title: "Create Account",
            register_message: "Join us to manage your home",
            forgot_title: "Reset Password",
            forgot_instructions: "Enter your email to reset your password.",
            btn_delete: "Delete",
            label_email: "Email",
            label_password: "Password",

            link_forgot: "Forgot password?",
            btn_connect: "Log In",

            text_no_account: "Don't have an account?",
            link_register: "Sign Up",
            text_have_account: "Already registered?",
            link_login: "Log In",

            btn_register_submit: "Create account",
            btn_forgot_submit: "Send link",
            link_back_login: "Back to login",

            p2_title: "Your Family Dashboard",
            p2_subtitle: "Organize your home easily",

            menu_find: "Find object",
            menu_reminders: "Reminders",
            menu_messages: "Messages",

            title_find: "Where is my item?",
            title_reminders: "Maintenance reminders",
            title_messages: "Family notes",

            btn_back: "➔ Back",

            obj_name: "Ex: Passport",
            obj_loc: "Ex: Drawer",

            rem_text: "Ex: Change filter",
            rem_days: "Days",

            msg_placeholder: "Ex: Important message..."
        }
    };

    let currentLang = "fr";

    function changeLanguage(lang) {

        currentLang = lang;

        const t = baseText[lang];
        if (!t) return;

        document.querySelectorAll("[data-i18n]").forEach(el => {
            const key = el.getAttribute("data-i18n");
            if (t[key]) el.textContent = t[key];
        });

        document.getElementById("objName")?.setAttribute("placeholder", t.obj_name);
        document.getElementById("objLoc")?.setAttribute("placeholder", t.obj_loc);
        document.getElementById("reminderText")?.setAttribute("placeholder", t.rem_text);
        document.getElementById("reminderDays")?.setAttribute("placeholder", t.rem_days);
        document.getElementById("msgText")?.setAttribute("placeholder", t.msg_placeholder);
        
        document.getElementById("searchObjInput")
?.setAttribute("placeholder", t.search_placeholder);

        updateModalHeader();
    }






// ===========================
// REMINDERS / MESSAGES FIRESTORE
// ===========================









    function updateModalHeader() {

        const t = baseText[currentLang];

        const title = document.getElementById("authTitle");
        const msg = document.getElementById("authMessage");

        if (!title || !msg) return;

        if (currentMode === "login") {
            title.textContent = t.login_title;
            msg.textContent = t.login_message;
        }

        else if (currentMode === "register") {
            title.textContent = t.register_title;
            msg.textContent = t.register_message;
        }

        else {
            title.textContent = t.forgot_title;
            msg.textContent = t.forgot_instructions;
        }
    }

    document.getElementById("langSelect")?.addEventListener("change", e => {
        changeLanguage(e.target.value);
    });

    



loginForm?.addEventListener("submit", async (e) => {

    e.preventDefault();

    const email =
        loginForm.querySelector('input[type="email"]').value;

    const password =
        loginForm.querySelector('input[type="password"]').value;

    try {

        await signInWithEmailAndPassword(
            auth,
            email,
            password
        );

        alert("Connexion réussie");

        loginSuccess();

    } catch (error) {

        alert(error.message);
    }
});
    
    
    
 registerForm?.addEventListener("submit", async (e) => {

    e.preventDefault();

    const email =
        registerForm.querySelector('input[type="email"]').value;

    const password =
        registerForm.querySelector('input[type="password"]').value;

    
   try {
    const userCredential = await createUserWithEmailAndPassword(auth, email, password);
    const user = userCredential.user;

    // 🔹 Générer un code familial unique
    const familyCode = generateFamilyCode();

    // 🔹 Sauvegarder l'utilisateur avec le code familial dans Firestore
    await setDoc(doc(db, "users", user.uid), {
        email: email,
        familyCode: familyCode,
        createdAt: Date.now()
    });

    alert(`Compte créé ! Votre code familial : ${familyCode}`);

    loginSuccess();

} catch (error) {
    alert(error.message);
} 
    
    
    
    
});   
    
    
    
    
    
    
    


    function openSub(page) {

        subPageFind?.classList.add("hidden");
        subPageReminders?.classList.add("hidden");
        subPageMessages?.classList.add("hidden");

        document.querySelector(".function-menu")?.classList.add("hidden");
        document.querySelector(".welcome-box")?.classList.add("hidden");

        page?.classList.remove("hidden");
    }

    function backMenu() {

        subPageFind?.classList.add("hidden");
        subPageReminders?.classList.add("hidden");
        subPageMessages?.classList.add("hidden");

        document.querySelector(".function-menu")?.classList.remove("hidden");
        document.querySelector(".welcome-box")?.classList.remove("hidden");
    }

    document.getElementById("btnGoFind")?.addEventListener("click", () => openSub(subPageFind));
    document.getElementById("btnGoReminders")?.addEventListener("click", () => openSub(subPageReminders));
    document.getElementById("btnGoMessages")?.addEventListener("click", () => openSub(subPageMessages));

    document.querySelectorAll(".btn-back").forEach(btn => {
        btn.addEventListener("click", backMenu);
    });

    window.objects = [];
    window.reminders = [];
    window.messages = [];
    
    
    
  async function loadObjects() {
    if (!auth.currentUser) return; // sécurité

    // 🔹 Récupérer le document de l'utilisateur connecté
    const userDocSnap = await getDoc(doc(db, "users", auth.currentUser.uid));
    if (!userDocSnap.exists()) return;

    const currentUserData = userDocSnap.data(); // contient email, familyCode, etc.
    const familyCode = currentUserData.familyCode; // 🔹 le code familial de ce foyer

    // 🔹 Récupérer tous les objets
    const snap = await getDocs(collection(db, "objects"));

    // 🔹 Filtrer seulement ceux de la même famille
    window.objects = snap.docs
        .map(d => ({ id: d.id, ...d.data() }))
        .filter(o => o.familyCode === familyCode);

    renderObjects();
}  
    
    
    
    


// Ajouter Reminder
document.getElementById("btnSubmitReminder")?.addEventListener("click", async () => {
    
    
    
    if (!auth.currentUser) {
    alert("Utilisateur non connecté");
    return;
}
    
    
    
    const t = document.getElementById("reminderText")?.value;
    const dateValue = document.getElementById("reminderDate")?.value;
    if (!t || !dateValue) return;

    // 🔹 Récupérer le familyCode
    const userDocSnap = await getDoc(doc(db, "users", auth.currentUser.uid));
    if (!userDocSnap.exists()) return;
    const familyCode = userDocSnap.data().familyCode;

    // 🔹 Ajouter le reminder avec familyCode
    await addDoc(collection(db, "reminders"), {
        userId: auth.currentUser.uid,
        familyCode: familyCode,
        text: t,
        date: dateValue,
        createdAt: Date.now()
    });

    document.getElementById("reminderText").value = "";
    document.getElementById("reminderDate").value = "";

    await loadReminders();
});







// Ajouter Message
document.getElementById("btnSubmitMsg")?.addEventListener("click", async () => {
    
    
    if (!auth.currentUser) {
    alert("Utilisateur non connecté");
    return;
}
    
    const text = document.getElementById("msgText")?.value?.trim();
    if (!text) return;

    // 🔹 Récupérer le familyCode
    const userDocSnap = await getDoc(doc(db, "users", auth.currentUser.uid));
    if (!userDocSnap.exists()) return;
    const familyCode = userDocSnap.data().familyCode;

    // 🔹 Ajouter le message avec familyCode
    await addDoc(collection(db, "messages"), {
        userId: auth.currentUser.uid,
        familyCode: familyCode,
        text,
        createdAt: Date.now()
    });

    document.getElementById("msgText").value = "";

    await loadMessages();
});

    
document.getElementById("btnSubmitObj")?.addEventListener("click", async () => {
    
    
    if (!auth.currentUser) {
    alert("Utilisateur non connecté");
    return;
}
    
    const n = document.getElementById("objName")?.value;
    const l = document.getElementById("objLoc")?.value;
    
    if (!n || !l) return;

    // 🔹 Récupérer le familyCode de l'utilisateur connecté
    const userDocSnap = await getDoc(doc(db, "users", auth.currentUser.uid));
    if (!userDocSnap.exists()) return;
    const familyCode = userDocSnap.data().familyCode;

    // 🔹 Ajouter l'objet avec familyCode
    await addDoc(collection(db, "objects"), {
        userId: auth.currentUser.uid,
        familyCode: familyCode,
        name: n,
        location: l,
        createdAt: Date.now()
    });
    
    document.getElementById("objName").value = "";
    document.getElementById("objLoc").value = "";

    loadObjects();
});
    
    
    

    
    
    
    

    
    
    
    document.getElementById("searchObjInput")?.addEventListener("input", (e) => {

    const value = normalizeText(e.target.value);

    document.querySelectorAll("#objectList .card-item").forEach(item => {

        const text = normalizeText(item.textContent);

        const match = text.includes(value) || similarity(text, value) > 0.6;

        item.style.display = match ? "flex" : "none";
    });
});




function normalizeText(text) {
    return text
        .toLowerCase()
        .normalize("NFD")
        .replace(/[\u0300-\u036f]/g, "")
        .replace(/[^a-z0-9]/g, "");
}

function similarity(a, b) {
    if (!a || !b) return 0;

    let longer = a.length > b.length ? a : b;
    let shorter = a.length > b.length ? b : a;

    let matches = 0;

    for (let i = 0; i < shorter.length; i++) {
        if (longer.includes(shorter[i])) matches++;
    }

    return matches / longer.length;
}
    
    
    
    function renderObjects() {

    const c = document.getElementById("objectList");
    if (!c) return;

    c.innerHTML = "";

    const sorted = [...window.objects].sort((a, b) =>
        a.name.toLowerCase().localeCompare(b.name.toLowerCase(), "fr", {
            sensitivity: "base"
        })
    );

    let currentLetter = "";

    sorted.forEach((o) => {

        const firstLetter = o.name.normalize("NFD").replace(/[\u0300-\u036f]/g, "").charAt(0).toUpperCase();

        if (firstLetter !== currentLetter) {

            currentLetter = firstLetter;

            const letter = document.createElement("div");
            letter.className = "letter-title";
            letter.textContent = currentLetter;

            c.appendChild(letter);
        }

        const card = document.createElement("div");
        card.className = "card-item";
        card.dataset.name = o.name.toLowerCase();

        const left = document.createElement("div");

        const strong = document.createElement("strong");
        strong.textContent = o.name;

        const small = document.createElement("small");
        small.textContent = o.location;

        left.appendChild(strong);
        left.appendChild(document.createElement("br"));
        left.appendChild(small);

           
           
           const btn = document.createElement("button");
btn.textContent = baseText[currentLang].btn_delete; // dynamique selon langue

btn.addEventListener("click", async () => {
    await deleteDoc(doc(db, "objects", o.id));
    loadObjects();
});
           
           
        

        card.appendChild(left);
        card.appendChild(btn);

        c.appendChild(card);
    });
}
    
    
function getBadge(days) {
    if (days <= 0) return "red";
    if (days <= 3) return "red";
    if (days <= 15) return "orange";
    return "green";
}




function generateFamilyCode() {
    const chars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789';
    let code = '';
    for (let i = 0; i < 8; i++) {
        code += chars.charAt(Math.floor(Math.random() * chars.length));
    }
    return code;
}





// =========================
// RENDERS CORRIGÉS
// =========================

function renderReminders() {
    const container = document.getElementById("reminderList");
    if (!container) return;

    container.innerHTML = "";

    // Calcul dynamique des jours restants
    const sorted = [...window.reminders].map(r => {
        const daysLeft = Math.ceil((new Date(r.date).getTime() - Date.now()) / (1000 * 60 * 60 * 24));
        return { ...r, daysLeft };
    }).sort((a, b) => a.daysLeft - b.daysLeft);

    sorted.forEach(r => {
        const badge = getBadge(r.daysLeft);

        let label = "";
        
        if (r.daysLeft < 0) {
    label = currentLang === "fr"
        ? `En retard de ${Math.abs(r.daysLeft)} jour(s)`
        : `${Math.abs(r.daysLeft)} day(s) overdue`;
} else {
    label = currentLang === "fr"
        ? `${r.daysLeft} jour(s) restants`
        : `${r.daysLeft} day(s) left`;
}
        
        

        const card = document.createElement("div");
        card.className = "card-item reminder-card";

        const top = document.createElement("div");
        top.className = "reminder-top";

        const title = document.createElement("strong");
        title.textContent = r.text;

        const span = document.createElement("span");
        span.className = `badge ${badge}`;
        span.textContent = label;

        top.appendChild(title);
        top.appendChild(span);

        const actions = document.createElement("div");
        actions.style.display = "flex";
        actions.style.gap = "8px";
        actions.style.marginTop = "8px";

        const delBtn = document.createElement("button");
        delBtn.textContent = baseText[currentLang].btn_delete;

        delBtn.addEventListener("click", async () => {
            await deleteDoc(doc(db, "reminders", r.id));
            await loadReminders();
        });

        actions.appendChild(delBtn);

        card.appendChild(top);
        card.appendChild(actions);

        container.appendChild(card);
    });
}



function renderMessages() {
    const container = document.getElementById("messageBoard");
    if (!container) return;

    container.innerHTML = "";

    const sorted = [...window.messages].reverse();

    sorted.forEach(m => {
        const card = document.createElement("div");
        card.className = "card-item message-card";

        const content = document.createElement("div");

        const text = document.createElement("p");
        text.textContent = m.text;

        const date = document.createElement("small");
        // Affichage correct de la date
        date.textContent = m.createdAt ? new Date(m.createdAt).toLocaleString() : "";

        content.appendChild(text);
        content.appendChild(date);

        const delBtn = document.createElement("button");
        delBtn.textContent = baseText[currentLang].btn_delete;

        delBtn.addEventListener("click", async () => {
            await deleteDoc(doc(db, "messages", m.id));
            await loadMessages();
        });

        card.appendChild(content);
        card.appendChild(delBtn);

        container.appendChild(card);
    });
}





// Charger reminders après login


async function loadReminders() {
    if (!auth.currentUser) return;

    const userDocSnap = await getDoc(doc(db, "users", auth.currentUser.uid));
    if (!userDocSnap.exists()) return;

    const currentUserData = userDocSnap.data();
    const familyCode = currentUserData.familyCode;

    const snap = await getDocs(collection(db, "reminders"));
    window.reminders = snap.docs
        .map(d => ({ id: d.id, ...d.data() }))
        .filter(r => r.familyCode === familyCode);

    renderReminders();
}







async function loadMessages() {
    if (!auth.currentUser) return;

    const userDocSnap = await getDoc(doc(db, "users", auth.currentUser.uid));
    if (!userDocSnap.exists()) return;

    const currentUserData = userDocSnap.data();
    const familyCode = currentUserData.familyCode;

    const snap = await getDocs(collection(db, "messages"));
    window.messages = snap.docs
        .map(d => ({ id: d.id, ...d.data() }))
        .filter(m => m.familyCode === familyCode);

    renderMessages();
}




// Appeler ces fonctions **après que l'utilisateur soit connecté**

async function loginSuccess() {
    closeModal();

    document.querySelector(".hero-container")?.classList.add("hidden");
    document.getElementById("page2")?.classList.remove("hidden");

    // 🔥 attendre que Firebase Auth soit bien prêt
    if (!auth.currentUser) return;

    await loadObjects();
    await loadReminders();
    await loadMessages();
}





    changeLanguage(document.getElementById("langSelect")?.value || "fr");

});
















