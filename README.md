# Play-List
HTML Code
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Song App</title>
    <link rel="icon" href="https://publicovationpr.wordpress.com/wp-content/uploads/2013/01/images.jpg">
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <h1>Song App</h1>
    <div class="playlist-container">
        <h2>Playlist</h2>
        <ul id="playlist"></ul>
    </div>
    <div class="controls">
        <button id="add-song-btn">Add Song</button>
        <button id="play-next-btn">Play Next</button>
        <button id="play-previous-btn">Play Previous</button>
        <select id="genre-select">
            <option value="All" >All</option>
            <option value="Rock" onclick="alert('Rahul')">Rock</option>
            <option value="Pop">Pop</option>
        </select>
    </div>
    <div class="song-details">
        <h2>Current Song</h2>
        <p id="current-song"></p>
    </div>

    <script src="script.js"></script>
</body>
</html>


JAVASCRIPT Code

// Initialize playlist and current song index
let playlist = [];
let currentSongIndex = -1;

// Function to add song to playlist
function addSong(title, artist, genre) {
    const song = { title, artist, genre };
    playlist.push(song);
    updatePlaylistUI();
}

// Function to play next song
function playNext() 
{
    if (currentSongIndex < playlist.length - 1) {
        currentSongIndex++;
        updateCurrentSongUI();
    }
}

// Function to play previous song
function playPrevious() {
    if (currentSongIndex > 0) {
        currentSongIndex--;
        updateCurrentSongUI();
    }
}

// Function to filter songs by genre
function filterByGenre(genre) {
    const filteredPlaylist = playlist.filter(song => song.genre === genre);
    updatePlaylistUI(filteredPlaylist);
}

// Function to update playlist UI
function updatePlaylistUI(filteredPlaylist = playlist) {
    const playlistElement = document.getElementById('playlist');
    playlistElement.innerHTML = '';
    filteredPlaylist.forEach(song => {
        const li = document.createElement('li');
        li.textContent = `${song.title} - ${song.artist} (${song.genre})`;
        playlistElement.appendChild(li);
    });
}

// Function to update current song UI
function updateCurrentSongUI() {
    const currentSongElement = document.getElementById('current-song');
    if (currentSongIndex >= 0 && currentSongIndex < playlist.length) {
        currentSongElement.textContent = `${playlist[currentSongIndex].title} - ${playlist[currentSongIndex].artist}`;
    } else {
        currentSongElement.textContent = '';
    }
}

// Event listeners
document.getElementById('add-song-btn').addEventListener('click', () => {
    const title = prompt('Enter song title:');
    const artist = prompt('Enter song artist:');
    const genre = prompt('Enter song genre:');
    addSong(title, artist, genre);
});

document.getElementById('play-next-btn').addEventListener('click', playNext);
document.getElementById('play-previous-btn').addEventListener('click', playPrevious);

document.getElementById('genre-select').addEventListener('change', event => {
    const selectedGenre = event.target.value;
    if (selectedGenre === 'All') {
        updatePlaylistUI();
    } else {
        filterByGenre(selectedGenre);
    }
});

// Initialize playlist with sample data
addSong('Song 1', 'Artist 1', 'Rock');
addSong('Song 2', 'Artist 2', 'Pop');
playNext(); // Start with first song



CSS Code
body {
    font-family: Arial, sans-serif;
}

.playlist-container {
    width: 50%;
    float: left;
}

.playlist-container ul {
    list-style: none;
    padding: 0;
    margin: 0;
}

.playlist-container li {
    padding: 10px;
    border-bottom: 1px solid #ccc;
}

.controls {
    width: 50%;
    float: right;
    text-align: right;
}

.controls button {
background-color: pink;
cursor: pointer;
    margin: 10px;
}

.song-details {
    background-color:greenyellow;
    clear: both;
    padding: 0.5px;
}

.song-details h2 {
    margin-top: 0;
}
