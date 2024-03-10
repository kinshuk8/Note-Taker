function saveNote() {
    const noteTitle = document.getElementById("noteTitle").value.trim();
    const noteContent = document.getElementById("noteContent").value.trim();
    
    if(!noteTitle || !noteContent) {
        alert("Don't leave them empty");
        return;
    }
    
    const note = {
        title: noteTitle,
        content: noteContent
    };
    
    let notes = JSON.parse(localStorage.getItem("notes")) || [];
    notes.push(note);
    
    localStorage.setItem("notes", JSON.stringify(notes));
    noteTitle.textContent = "";
    noteContent.textContent = "";
    displayNotes();
}

function displayNotes() {
    let notes = JSON.parse(localStorage.getItem("notes")) || [];
    const notesList = document.getElementById("notesList");
    notesList.innerHTML = "";
    const template = document.getElementById("noteTemplate");
    
    notes.forEach(note => {
        const clone = document.importNode(template.content, true);
        clone.querySelector(".note-title").textContent = note.title;
        clone.querySelector(".note-content").textContent = note.content;
        notesList.appendChild(clone);
    });
}

function deleteNote() {
    const checkboxes = document.querySelectorAll('.note-checkbox:checked');
    checkboxes.forEach(checkbox => {
        const listItem = checkbox.closest('.note');
        listItem.remove();
        
        const noteTitle = listItem.querySelector('.note-title').textContent;
        const noteContent = listItem.querySelector('.note-content').textContent;
        removeNoteFromLocalStorage(noteTitle, noteContent);
    });
}

function removeNoteFromLocalStorage(title, content) {
    let notes = JSON.parse(localStorage.getItem("notes")) || [];
    notes = notes.filter(note => !(note.title === title && note.content === content));
    localStorage.setItem("notes", JSON.stringify(notes));
}

function clearAllNotes() {
    localStorage.removeItem("notes");
    displayNotes();
}

function searchNotes() {
    const searchText = document.getElementById("search").value.trim().toLowerCase();
    let filteredNotes = [];
    if (searchText) {
        const notes = JSON.parse(localStorage.getItem("notes")) || [];
        filteredNotes = notes.filter(note => {
            return note.title.toLowerCase().includes(searchText) || note.content.toLowerCase().includes(searchText);
        });
    }
    displayFilteredNotes(filteredNotes);
}

function displayFilteredNotes(filteredNotes) {
    const notesList = document.getElementById("notesList");
    notesList.innerHTML = "";
    filteredNotes.forEach(note => {
        const listItem = document.createElement("div");
        listItem.classList.add("note");
        listItem.innerHTML = `
            <input type="checkbox" class="note-checkbox">
            <h3 class="note-title">${note.title}</h3>
            <p class="note-content">${note.content}</p>
            <hr>
        `;
        notesList.appendChild(listItem);
    });
}
