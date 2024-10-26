<html>
<head>
    <title>Premium NFT Gallery</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.0/gsap.min.js"></script>
    <style>
        :root {
            --primary-color: #A67C00;
            --primary-hover: #8B6914;
            --accent-gold: #FFD700;
            --background-dark: #0A0B0E;
            --card-bg: #141519;
            --text-light: #FFFFFF;
            --text-gold: #D4AF37;
            --premium-gradient: linear-gradient(135deg, #B8860B, #FFD700);
            --card-shadow: 0 8px 32px rgba(0, 0, 0, 0.4);
            --glass-effect: rgba(255, 255, 255, 0.05);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            min-height: 100vh;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: var(--background-dark);
            color: var(--text-light);
            background-image: 
                radial-gradient(circle at 20% 20%, rgba(255, 215, 0, 0.05) 0%, transparent 40%),
                radial-gradient(circle at 80% 80%, rgba(255, 215, 0, 0.05) 0%, transparent 40%);
            overflow-x: hidden;
            padding: 80px 20px 20px;
        }

        .header {
            padding: 20px;
            background: rgba(0, 0, 0, 0.8);
            backdrop-filter: blur(20px);
            position: fixed;
            width: 100%;
            top: 0;
            left: 0;
            z-index: 1000;
            border-bottom: 1px solid rgba(255, 215, 0, 0.1);
        }

        .header-content {
            max-width: 1400px;
            margin: 0 auto;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            font-size: 1.8em;
            font-weight: 800;
            background: var(--premium-gradient);
            -webkit-background-clip: text;
            color: transparent;
            letter-spacing: 1px;
        }

        .connect-wallet {
            padding: 10px 20px;
            background: var(--premium-gradient);
            border: none;
            border-radius: 25px;
            color: var(--background-dark);
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .connect-wallet:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(255, 215, 0, 0.2);
        }

        .gallery-container {
            height: 600px;
            margin: 100px auto 40px;
            padding: 20px;
            position: relative;
            overflow: hidden;
        }

        .carousel-wrapper {
            display: flex;
            gap: 30px;
            position: absolute;
            transition: transform 0.5s ease-out;
            padding: 20px;
        }

        .artwork-card {
            min-width: 400px;
            height: 550px;
            background: var(--card-bg);
            border-radius: 20px;
            overflow: hidden;
            box-shadow: var(--card-shadow);
            transition: all 0.4s ease;
            border: 1px solid rgba(255, 215, 0, 0.1);
            cursor: pointer;
        }

        .artwork-card:hover {
            transform: translateY(-10px) scale(1.02);
            box-shadow: 0 15px 40px rgba(255, 215, 0, 0.1);
        }

        .artwork-image {
            position: relative;
            width: 100%;
            height: 300px;
            overflow: hidden;
        }

        .artwork-image img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: transform 0.5s ease;
        }

        .artwork-card:hover .artwork-image img {
            transform: scale(1.05);
        }

        .premium-badge {
            position: absolute;
            top: 20px;
            right: 20px;
            background: var(--premium-gradient);
            padding: 8px 16px;
            border-radius: 25px;
            font-size: 0.9em;
            font-weight: bold;
            color: var(--background-dark);
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
        }

        .price-tag {
            position: absolute;
            bottom: 20px;
            left: 20px;
            background: rgba(0, 0, 0, 0.8);
            padding: 10px 20px;
            border-radius: 15px;
            color: var(--text-gold);
            font-weight: bold;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 215, 0, 0.2);
        }

        .artwork-info {
            padding: 25px;
            background: linear-gradient(to bottom, rgba(20, 21, 25, 0.8), rgba(10, 11, 14, 0.9));
        }

        .artwork-title {
            font-size: 1.4em;
            color: var(--text-gold);
            margin-bottom: 10px;
            font-weight: bold;
        }

        .artwork-collection {
            color: rgba(255, 255, 255, 0.7);
            font-size: 0.9em;
            margin-bottom: 15px;
        }

        .action-buttons {
            display: flex;
            gap: 15px;
            margin-top: 20px;
        }

        .action-btn {
            flex: 1;
            padding: 12px;
            border: none;
            border-radius: 12px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .buy-btn {
            background: var(--premium-gradient);
            color: var(--background-dark);
        }

        .view-btn {
            background: var(--glass-effect);
            color: var(--text-light);
            border: 1px solid rgba(255, 215, 0, 0.2);
        }

        .action-btn:hover {
            transform: translateY(-2px);
        }

        .carousel-nav {
            position: absolute;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%);
            display: flex;
            gap: 10px;
            z-index: 100;
        }

        .nav-btn {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: rgba(0, 0, 0, 0.5);
            border: 1px solid var(--text-gold);
            color: var(--text-gold);
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .nav-btn:hover {
            background: var(--premium-gradient);
            color: var(--background-dark);
        }

        .modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.9);
            backdrop-filter: blur(10px);
            display: none;
            justify-content: center;
            align-items: center;
            z-index: 2000;
        }

        .modal-content {
            background: var(--card-bg);
            width: 90%;
            max-width: 1000px;
            border-radius: 20px;
            padding: 30px;
            position: relative;
            border: 1px solid rgba(255, 215, 0, 0.2);
        }

        .modal-close {
            position: absolute;
            top: 20px;
            right: 20px;
            background: none;
            border: none;
            color: var(--text-light);
            font-size: 24px;
            cursor: pointer;
        }

        .modal-details {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
        }

        .modal-image {
            width: 100%;
            height: 400px;
            border-radius: 15px;
            overflow: hidden;
        }

        .modal-image img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        .modal-info {
            display: flex;
            flex-direction: column;
            gap: 20px;
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
            margin-top: 20px;
        }

        .stat-item {
            background: rgba(255, 255, 255, 0.05);
            padding: 15px;
            border-radius: 10px;
            text-align: center;
        }

        .stat-label {
            color: var(--text-gold);
            font-size: 0.9em;
            margin-bottom: 5px;
        }

        .stat-value {
            font-size: 1.2em;
            font-weight: bold;
        }

        @media (max-width: 768px) {
            .artwork-card {
                min-width: 300px;
            }

            .modal-details {
                grid-template-columns: 1fr;
            }

            .modal-image {
                height: 300px;
            }
        }
    </style>
</head>
<body>
    <header class="header">
        <div class="header-content">
            <div class="logo">GENESIS</div>
            <button class="connect-wallet">
                <i class="fas fa-wallet"></i>
                Connect
            </button>
        </div>
    </header>

    <div class="gallery-container">
        <div class="carousel-wrapper">
            <!-- NFT Cards will be dynamically inserted here -->
        </div>
        <div class="carousel-nav">
            <button class="nav-btn prev-btn"><i class="fas fa-chevron-left"></i></button>
            <button class="nav-btn next-btn"><i class="fas fa-chevron-right"></i></button>
        </div>
    </div>

    <div class="modal">
        <div class="modal-content">
            <button class="modal-close"><i class="fas fa-times"></i></button>
            <div class="modal-details">
                <!-- Modal content will be dynamically inserted here -->
            </div>
        </div>
    </div>

    <script>
        const nftData = [
            {
                id: 1,
                title: "Divine Harmony #001",
                collection: "Genesis Collection",
                price: "12.5 ETH",
                image: "https://i.ibb.co/yFNbRqF/Whats-App-Image-2024-10-20-at-09-16-07-510389dd.jpg",
                badge: "Genesis Edition",
                creator: "CryptoMaster",
                views: "1.2K",
                likes: "856",
                created: "2024-03-15"
            },
            {
                id: 2,
                title: "Ethereal Dreams #002",
                collection: "Platinum Series",
                price: "8.8 ETH",
                image: "https://i.ibb.co/7vkRDZv/Whats-App-Image-2024-10-20-at-09-16-08-0798f91f.jpg",
                badge: "Platinum",
                creator: "ArtVision",
                views: "987",
                likes: "654",
                created: "2024-03-16"
            },
            {
                id: 3,
                title: "Quantum Legacy #003",
                collection: "Elite Collection",
                price: "15.2 ETH",
                image: "https://i.ibb.co/k8zNj9j/a-captivating-and-dreamlike-scene-of-a-dali-esque-swof-qz-GQu-Ks-Sj-h-EVGflw-q-Em-M-hmr-Rcm-FUZb-GUc.jpg",
                badge: "Ultra Rare",
                creator: "QuantumArt",
                views: "2.1K",
                likes: "1.5K",
                created: "2024-03-17"
            },
            {
                id: 4,
                title: "Celestial Vision #004",
                collection: "Masterpiece Series",
                price: "18.5 ETH",
                image: "https://i.ibb.co/k51wwwg/an-awe-inspiring-scene-of-mythical-beasts-roaming-E6-Ugt4-g-TAO4r-Pl-Gpra-e-Q-t0tr-Egk6-Sf2r8k-Tr2-I.jpg",
                badge: "Masterpiece",
                creator: "StardustStudio",
                views: "1.8K",
                likes: "1.2K",
                created: "2024-03-18"
            },
            {
                id: 5,
                title: "Digital Royalty #005",
                collection: "Crown Collection",
                price: "21.0 ETH",
                image: "https://i.ibb.co/YBXK5Mg/a-striking-3d-illustration-of-a-t-shirt-hanging-on-h1-AIHpnz-TRK-8e-SADc-LFJw-l-Hs-Od-YYj-Sp-Wg6xv-U.jpg",
                badge: "Royal Edition",
                creator: "CrownMaster",
                views: "2.5K",
                likes: "1.8K",
                created: "2024-03-19"
            }
        ];

        function createNFTCard(nft) {
            return `
                <div class="artwork-card" data-id="${nft.id}">
                    <div class="artwork-image">
                        <div class="premium-badge">${nft.badge}</div>
                        <div class="price-tag">
                            <i class="fab fa-ethereum"></i> ${nft.price}
                        </div>
<img src="${nft.image}" alt="${nft.title}">
                    </div>
                    <div class="artwork-info">
                        <h3 class="artwork-title">${nft.title}</h3>
                        <p class="artwork-collection">${nft.collection}</p>
                        <p class="artwork-creator">By ${nft.creator}</p>
                        <div class="action-buttons">
                            <button class="action-btn buy-btn">Purchase Now</button>
                            <button class="action-btn view-btn">View Details</button>
                        </div>
                    </div>
                </div>
            `;
        }

        function createModalContent(nft) {
            return `
                <div class="modal-image">
                    <img src="${nft.image}" alt="${nft.title}">
                </div>
                <div class="modal-info">
                    <div class="premium-badge">${nft.badge}</div>
                    <h2 class="artwork-title">${nft.title}</h2>
                    <p class="artwork-collection">${nft.collection}</p>
                    <p class="artwork-creator">Created by ${nft.creator}</p>
                    <div class="stats-grid">
                        <div class="stat-item">
                            <div class="stat-label">Price</div>
                            <div class="stat-value"><i class="fab fa-ethereum"></i> ${nft.price}</div>
                        </div>
                        <div class="stat-item">
                            <div class="stat-label">Views</div>
                            <div class="stat-value">${nft.views}</div>
                        </div>
                        <div class="stat-item">
                            <div class="stat-label">Likes</div>
                            <div class="stat-value">${nft.likes}</div>
                        </div>
                        <div class="stat-item">
                            <div class="stat-label">Created</div>
                            <div class="stat-value">${new Date(nft.created).toLocaleDateString()}</div>
                        </div>
                    </div>
                    <div class="action-buttons">
                        <button class="action-btn buy-btn">Purchase Now</button>
                        <button class="action-btn view-btn">
                            <i class="far fa-heart"></i> Add to Favorites
                        </button>
                    </div>
                </div>
            `;
        }

        class NFTGallery {
            constructor() {
                this.currentIndex = 0;
                this.wrapper = document.querySelector('.carousel-wrapper');
                this.cards = [];
                this.modal = document.querySelector('.modal');
                this.initializeGallery();
                this.setupEventListeners();
            }

            initializeGallery() {
                this.wrapper.innerHTML = nftData.map(nft => createNFTCard(nft)).join('');
                this.cards = document.querySelectorAll('.artwork-card');
                this.updateCarousel();
            }

            setupEventListeners() {
                // Navigation buttons
                document.querySelector('.prev-btn').addEventListener('click', () => this.navigate(-1));
                document.querySelector('.next-btn').addEventListener('click', () => this.navigate(1));

                // Modal events
                this.cards.forEach(card => {
                    card.addEventListener('click', () => this.openModal(card.dataset.id));
                });

                document.querySelector('.modal-close').addEventListener('click', () => this.closeModal());

                // Keyboard navigation
                document.addEventListener('keydown', (e) => {
                    if (e.key === 'ArrowLeft') this.navigate(-1);
                    if (e.key === 'ArrowRight') this.navigate(1);
                    if (e.key === 'Escape') this.closeModal();
                });

                // Touch events for mobile
                let touchStartX = 0;
                let touchEndX = 0;

                this.wrapper.addEventListener('touchstart', (e) => {
                    touchStartX = e.changedTouches[0].screenX;
                });

                this.wrapper.addEventListener('touchend', (e) => {
                    touchEndX = e.changedTouches[0].screenX;
                    if (touchStartX - touchEndX > 50) this.navigate(1);
                    if (touchStartX - touchEndX < -50) this.navigate(-1);
                });
            }

            navigate(direction) {
                this.currentIndex = (this.currentIndex + direction + nftData.length) % nftData.length;
                this.updateCarousel();
            }

            updateCarousel() {
                const cardWidth = this.cards[0].offsetWidth + 30; // Including gap
                const offset = -this.currentIndex * cardWidth;
                gsap.to(this.wrapper, {
                    x: offset,
                    duration: 0.5,
                    ease: "power2.out"
                });
            }

            openModal(id) {
                const nft = nftData.find(item => item.id === parseInt(id));
                document.querySelector('.modal-details').innerHTML = createModalContent(nft);
                gsap.fromTo(this.modal, 
                    { opacity: 0 }, 
                    { 
                        opacity: 1, 
                        duration: 0.3,
                        display: 'flex'
                    }
                );
            }

            closeModal() {
                gsap.to(this.modal, {
                    opacity: 0,
                    duration: 0.3,
                    onComplete: () => {
                        this.modal.style.display = 'none';
                    }
                });
            }
        }

        // Initialize gallery when the page loads
        window.addEventListener('load', () => {
            new NFTGallery();
            
            // Add smooth scroll animation to connect wallet button
            document.querySelector('.connect-wallet').addEventListener('click', () => {
                gsap.to(this, {
                    duration: 0.5,
                    ease: "power2.out",
                    onStart: () => {
                        // Add wallet connection logic here
                        alert('Wallet connection feature would be implemented here');
                    }
                });
            });
        });
    </script>
</body>
