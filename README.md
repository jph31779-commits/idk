import React, { useState, useEffect } from 'react';
import { Shield, ArrowUpRight, ShoppingCart, Camera, Menu, X, Instagram, Linkedin, FileText } from 'lucide-react';

const App = () => {
  const [selectedImage, setSelectedImage] = useState(null);
  const [isScrolled, setIsScrolled] = useState(false);
  const [imagesLoaded, setImagesLoaded] = useState({ logo: true, hero: true, signature: true });

  // --- 1. ASSET CONFIGURATION (GITHUB READY) ---
  // To populate with your real photos:
  // 1. Place your images in the 'public' or 'assets' folder of your repo.
  // 2. Uncomment the lines below and point them to your filenames.
  
  // const LOGO_FILENAME = "./B0641B0D-0CC1-4EB0-A36E-49191CC4D9F8_4_5005_c.jpeg";
  // const SIGNATURE_FILENAME = "./B1C98395-D8E2-4629-9A51-2EE47EC7A731_4_5005_c.jpeg";
  // const HERO_FILENAME = "./image_136e9b.png"; 
  // const SCANNED_IMG_1 = "./IMG_0136.JPG"; // From your 2011 scan
  // const SCANNED_IMG_2 = "./IMG_0060.JPG"; // From your 2011 scan
  // const SCANNED_IMG_3 = "./IMG_0120.JPG"; // From your 2011 scan

  // --- 2. PLACEHOLDERS (ACTIVE FOR DEPLOYMENT) ---
  const LOGO_FILENAME = null; // Forces the Nickel Text Logo if file missing
  const SIGNATURE_FILENAME = null;
  const HERO_FILENAME = "https://images.unsplash.com/photo-1470071459604-3b5ec3a7fe05?q=80&w=2072&auto=format&fit=crop";
  
  // Scanned photo placeholders
  const SCANNED_IMG_1 = "https://images.unsplash.com/photo-1511497584788-876760111969?q=80&w=1932&auto=format&fit=crop";
  const SCANNED_IMG_2 = "https://images.unsplash.com/photo-1447752875215-b2761acb3c5d?q=80&w=1740&auto=format&fit=crop";
  const SCANNED_IMG_3 = "https://images.unsplash.com/photo-1441974231531-c6227db76b6e?q=80&w=1740&auto=format&fit=crop";

  useEffect(() => {
    // Injecting Luxury Fonts: Bodoni Moda (Serif) & Montserrat (Sans)
    const link = document.createElement('link');
    link.href = 'https://fonts.googleapis.com/css2?family=Bodoni+Moda:ital,opsz,wght@0,6..96,400;0,6..96,500;0,6..96,600;0,6..96,700;1,6..96,400;1,6..96,700&family=Montserrat:wght@200;300;400;500;600&display=swap';
    link.rel = 'stylesheet';
    document.head.appendChild(link);

    const handleScroll = () => setIsScrolled(window.scrollY > 50);
    window.addEventListener('scroll', handleScroll);
    return () => window.removeEventListener('scroll', handleScroll);
  }, []);

  // --- 3. GALLERY DATA ---
  const photos = [
    { id: 1, url: SCANNED_IMG_1, title: 'Perspective Study I', category: 'Fine Art', span: 'col-span-1 md:col-span-2 row-span-2', price: '$1,200' },
    { id: 2, url: HERO_FILENAME, title: 'Visual Rhythm', category: 'Limited', span: 'col-span-1 row-span-1', price: '$850' },
    { id: 3, url: SCANNED_IMG_2, title: 'Depth Analysis', category: 'Exclusive', span: 'col-span-1 row-span-2', price: '$2,400' },
    { id: 4, url: HERO_FILENAME, title: 'The Modern Frame', category: 'Standard', span: 'col-span-1 row-span-1', price: '$450' },
    { id: 5, url: SCANNED_IMG_3, title: 'Hart Collection 05', category: 'Series', span: 'col-span-1 md:col-span-2 row-span-1', price: '$900' },
  ];

  // --- 4. STYLES (BRUSHED NICKEL) ---
  
  // Nickel Filter for IMAGES (Inverts White to Transparent Black -> Nickel)
  const nickelFilter = {
    filter: 'invert(1) grayscale(1) brightness(0.7) contrast(1.3)',
    mixBlendMode: 'screen',
  };

  // Nickel Gradient for TEXT Fallback (if image breaks)
  const nickelText = {
    background: 'linear-gradient(to bottom, #e0e0e0 0%, #888888 100%)',
    WebkitBackgroundClip: 'text',
    WebkitTextFillColor: 'transparent',
    textShadow: '0px 1px 2px rgba(255,255,255,0.2)',
    fontFamily: "'Bodoni Moda', serif"
  };

  const fontSerif = { fontFamily: "'Bodoni Moda', serif" };
  const fontSans = { fontFamily: "'Montserrat', sans-serif" };

  // Fallback handler
  const handleImageError = (type) => {
    setImagesLoaded(prev => ({ ...prev, [type]: false }));
  };

  return (
    <div className="min-h-screen bg-[#050505] text-[#d4d4d4] selection:bg-stone-600 selection:text-white overflow-x-hidden">
      
      {/* --- NAVIGATION --- */}
      <nav className={`fixed top-0 w-full z-50 transition-all duration-700 px-6 md:px-12 py-6 ${isScrolled ? 'bg-[#050505]/95 backdrop-blur-xl border-b border-white/5 py-4' : 'bg-transparent'}`}>
        <div className="max-w-[1920px] mx-auto flex justify-between items-center">
          
          <div className="flex items-center gap-5 group cursor-pointer">
            <div className="relative w-16 h-16 flex items-center justify-center">
              {imagesLoaded.logo ? (
                <img 
                  src={LOGO_FILENAME} 
                  alt="Hart Logo" 
                  className="w-full h-full object-contain transition-transform duration-700 group-hover:scale-110"
                  style={nickelFilter}
                  onError={() => handleImageError('logo')}
                />
              ) : (
                <h1 className="text-3xl italic font-bold tracking-tighter" style={nickelText}>H</h1>
              )}
            </div>
            <div className="flex flex-col justify-center">
              <h1 className="text-xl tracking-tighter leading-none text-white uppercase italic" style={fontSerif}>Hart</h1>
              <span className="text-[9px] uppercase tracking-[0.4em] text-[#888] mt-1" style={fontSans}>Photography</span>
            </div>
          </div>
          
          <div className="flex items-center gap-12" style={fontSans}>
            <div className="hidden lg:flex gap-12 text-[10px] uppercase tracking-[0.3em] font-medium text-[#888]">
              <a href="#anthology" className="hover:text-white transition-colors duration-300">Anthology</a>
              <a href="#licensing" className="hover:text-white transition-colors duration-300">Rights</a>
              <a href="#contact" className="hover:text-white transition-colors duration-300">Collab</a>
            </div>
            <button className="flex items-center gap-3 px-5 py-2 border border-white/10 rounded-sm hover:bg-white hover:text-black transition-all duration-300 group">
              <span className="text-[10px] uppercase tracking-[0.2em] font-bold">Vault</span>
              <div className="w-1 h-1 bg-[#888] rounded-full group-hover:bg-black transition-colors"></div>
            </button>
          </div>
        </div>
      </nav>

      {/* --- HERO SECTION --- */}
      <section className="relative h-screen w-full flex items-center justify-center bg-black overflow-hidden">
        
        {/* Floating Image Layer */}
        <div className="absolute inset-0 flex items-center justify-center p-0 md:p-8 lg:p-12">
          <div className="relative w-full h-full max-w-[1600px] overflow-hidden shadow-2xl bg-[#080808]">
            <img 
              src={imagesLoaded.hero ? HERO_FILENAME : "https://images.unsplash.com/photo-1493301865958-3d712cb0718d?auto=format&fit=crop&q=80"}
              alt="Hero Perspective" 
              className="w-full h-full object-cover opacity-60"
              onError={() => handleImageError('hero')}
            />
            {/* Voids */}
            <div className="absolute inset-0 bg-[radial-gradient(circle_at_center,_transparent_20%,_#000000_100%)] opacity-80"></div>
            <div className="absolute inset-0 bg-gradient-to-t from-black via-transparent to-black opacity-90"></div>
          </div>
        </div>

        {/* Content Layer (Riding on top) */}
        <div className="relative z-10 flex flex-col items-center justify-center text-center px-4 w-full">
          
          {/* LOGO CENTERPIECE */}
          <div className="w-56 h-56 md:w-80 md:h-80 mb-6 flex items-center justify-center opacity-90 animate-pulse-slow">
             {imagesLoaded.logo ? (
                <img 
                  src={LOGO_FILENAME} 
                  className="w-full h-full object-contain" 
                  style={nickelFilter} 
                  alt="Main Logo"
                  onError={() => handleImageError('logo')}
                />
             ) : (
                <h1 className="text-[140px] md:text-[220px] italic font-bold tracking-tighter" style={nickelText}>Hart</h1>
             )}
          </div>

          <h2 className="text-[10px] md:text-[12px] uppercase tracking-[1em] text-[#666] mb-8 font-medium" style={fontSans}>
            Perspectives from the Hart Photography
          </h2>

          <h1 className="text-[3.5rem] md:text-[6rem] lg:text-[7rem] leading-[0.9] text-[#e5e5e5] italic drop-shadow-xl" style={fontSerif}>
            Showing you the world <br />
            <span className="text-[1.5rem] md:text-[2.5rem] not-italic font-light tracking-wide text-[#999] block mt-4" style={fontSans}>
              from a different perspective.
            </span>
          </h1>
        </div>
      </section>

      {/* --- ANTHOLOGY GRID --- */}
      <section id="anthology" className="relative py-32 px-6 md:px-12 bg-[#050505]">
        <div className="max-w-[1920px] mx-auto">
          <div className="flex flex-col md:flex-row justify-between items-end mb-20 pb-12 border-b border-white/5">
            <div>
              <h2 className="text-6xl md:text-8xl italic text-white mb-4" style={fontSerif}>The Store</h2>
              <p className="text-[11px] uppercase tracking-[0.4em] text-[#666]" style={fontSans}>Curated Visual Assets</p>
            </div>
            <div className="hidden md:block text-right">
              <Camera className="text-[#333] mb-4 ml-auto" size={48} strokeWidth={1} />
              <p className="text-2xl text-white italic" style={fontSerif}>Vol. MMXXVI</p>
            </div>
          </div>

          <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 auto-rows-[400px] md:auto-rows-[600px] gap-8">
            {photos.map((photo) => (
              <div 
                key={photo.id}
                className={`${photo.span} group relative bg-[#080808] overflow-hidden cursor-none`}
                onClick={() => setSelectedImage(photo)}
              >
                <img 
                  src={photo.url}
                  alt={photo.title}
                  className="w-full h-full object-cover opacity-50 group-hover:opacity-100 transition-all duration-[1.5s] ease-out group-hover:scale-105"
                  onError={(e) => e.target.src = "https://images.unsplash.com/photo-1470071459604-3b5ec3a7fe05?auto=format&fit=crop&q=80"}
                />
                
                {/* Watermark Logo */}
                <div className="absolute top-8 left-8 w-12 h-12 opacity-0 group-hover:opacity-50 transition-opacity duration-700 flex items-center justify-center">
                  {imagesLoaded.logo ? (
                    <img src={LOGO_FILENAME} className="w-full h-full object-contain" style={nickelFilter} alt="" />
                  ) : (
                    <span className="text-2xl font-bold italic opacity-50" style={nickelText}>H</span>
                  )}
                </div>

                <div className="absolute inset-0 p-8 md:p-12 flex flex-col justify-between pointer-events-none">
                  <div className="flex justify-between items-start translate-y-[-20px] opacity-0 group-hover:translate-y-0 group-hover:opacity-100 transition-all duration-500">
                    <span className="px-4 py-1 bg-white text-black text-[9px] uppercase tracking-widest font-bold">{photo.category}</span>
                  </div>
                  
                  <div className="translate-y-[20px] opacity-0 group-hover:translate-y-0 group-hover:opacity-100 transition-all duration-500 delay-100">
                    <h3 className="text-3xl md:text-4xl italic text-white mb-2" style={fontSerif}>{photo.title}</h3>
                    <div className="flex justify-between items-end border-t border-white/20 pt-4">
                      <p className="text-xl text-[#ccc]" style={fontSerif}>{photo.price}</p>
                      <div className="flex items-center gap-2 text-[10px] uppercase tracking-[0.3em] text-white">
                        <span>Acquire</span> <ArrowUpRight size={14} />
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            ))}
          </div>
        </div>
      </section>

      {/* --- LICENSING --- */}
      <section id="licensing" className="py-32 px-6 md:px-12 bg-[#020202] border-t border-white/5">
        <div className="max-w-[1600px] mx-auto grid lg:grid-cols-12 gap-12 lg:gap-24 items-center">
          
          <div className="lg:col-span-5">
            <div className="w-24 h-24 mb-12 opacity-80 flex items-center justify-center">
               {imagesLoaded.logo ? (
                  <img src={LOGO_FILENAME} className="w-full h-full object-contain" style={nickelFilter} alt="" />
               ) : (
                  <h1 className="text-6xl italic font-bold" style={nickelText}>H</h1>
               )}
            </div>
            <h2 className="text-6xl md:text-8xl italic text-white mb-8 leading-[0.9]" style={fontSerif}>
              Visual <br/> Equity.
            </h2>
            <p className="text-lg text-[#888] font-light leading-relaxed mb-12" style={fontSans}>
              Every frame in the Hart Archive is a protected intellectual asset. We offer bespoke licensing tiers for brands requiring authentic, high-value imagery.
            </p>
            <button className="px-12 py-5 bg-white text-black hover:bg-[#ccc] transition-colors text-[11px] uppercase tracking-[0.3em] font-bold">
              View Rate Card
            </button>
          </div>

          <div className="lg:col-span-7 grid gap-6">
            {[
              { title: 'Commercial License', desc: 'Global buyout for advertising, packaging, and digital identity.' },
              { title: 'Editorial Rights', desc: 'Single-use rights for periodicals, publishing, and journalism.' },
              { title: 'Private Collection', desc: 'Signed archival prints for interior design and private display.' }
            ].map((item, i) => (
              <div key={i} className="group p-10 border border-white/5 hover:border-white/20 hover:bg-white/[0.02] transition-all cursor-pointer">
                <div className="flex justify-between items-center mb-4">
                  <h3 className="text-3xl italic text-white" style={fontSerif}>{item.title}</h3>
                  <ArrowUpRight className="text-[#666] group-hover:text-white transition-colors" />
                </div>
                <p className="text-sm text-[#666] font-light tracking-wide" style={fontSans}>{item.desc}</p>
              </div>
            ))}
          </div>

        </div>
      </section>

      {/* --- FOOTER --- */}
      <footer id="contact" className="py-24 px-6 md:px-12 bg-black border-t border-white/5">
        <div className="max-w-[1920px] mx-auto flex flex-col md:flex-row justify-between items-end gap-20">
          
          <div className="max-w-2xl">
            <h2 className="text-[11px] uppercase tracking-[0.6em] text-[#666] mb-8" style={fontSans}>The Collab</h2>
            <a href="mailto:Joshua@pfthphotography.com" className="text-4xl md:text-6xl lg:text-7xl italic text-white hover:text-[#aaa] transition-colors leading-none block mb-12" style={fontSerif}>
              Joshua@pfth<br/>photography.com
            </a>
          </div>

          <div className="flex flex-col items-center md:items-end">
             <div className="w-64 md:w-96 mb-8 flex justify-end">
               {imagesLoaded.signature ? (
                 <img 
                   src={SIGNATURE_FILENAME} 
                   className="w-full h-full object-contain opacity-50 hover:opacity-100 transition-opacity duration-500" 
                   style={nickelFilter} 
                   alt="Signature"
                   onError={() => handleImageError('signature')}
                 />
               ) : (
                  <div className="text-right">
                    <p className="text-5xl italic text-[#666] font-bold tracking-tighter" style={nickelText}>Hart.</p>
                  </div>
               )}
             </div>
             <p className="text-[9px] uppercase tracking-[0.4em] text-[#444]" style={fontSans}>
               © 2026 Hart Perspectives • All Rights Reserved
             </p>
          </div>

        </div>
      </footer>

      {/* --- MODAL --- */}
      {selectedImage && (
        <div className="fixed inset-0 z-[100] bg-black/95 backdrop-blur-xl flex items-center justify-center p-4">
          <button 
            onClick={() => setSelectedImage(null)}
            className="absolute top-8 right-8 text-white hover:text-[#888] transition-colors"
          >
            <X size={32} />
          </button>
          
          <div className="w-full max-w-7xl grid grid-cols-1 lg:grid-cols-2 gap-12 items-center">
            <div className="relative aspect-square lg:aspect-[4/5] bg-[#0a0a0a]">
              <img 
                 src={imagesLoaded.hero ? selectedImage.url : "https://images.unsplash.com/photo-1470071459604-3b5ec3a7fe05?auto=format&fit=crop&q=80"}
                 alt={selectedImage.title} 
                 className="w-full h-full object-contain" 
                 onError={(e) => e.target.src="https://images.unsplash.com/photo-1470071459604-3b5ec3a7fe05?auto=format&fit=crop&q=80"}
              />
            </div>
            
            <div className="text-left">
              <span className="inline-block px-3 py-1 border border-[#333] text-[#888] text-[9px] uppercase tracking-[0.2em] mb-6" style={fontSans}>
                {selectedImage.category}
              </span>
              <h2 className="text-6xl italic text-white mb-4" style={fontSerif}>{selectedImage.title}</h2>
              <p className="text-4xl text-[#ccc] mb-12" style={fontSerif}>{selectedImage.price}</p>
              
              <div className="flex flex-col gap-4 max-w-md" style={fontSans}>
                <button className="w-full py-4 bg-white text-black text-[10px] uppercase tracking-[0.3em] font-bold hover:bg-[#ccc] transition-colors">
                  Add to Vault
                </button>
              </div>

              <div className="mt-12 flex items-center gap-4 opacity-50">
                 <Shield size={16} />
                 <span className="text-[10px] uppercase tracking-[0.2em]" style={fontSans}>Verified Hart Original</span>
              </div>
            </div>
          </div>
        </div>
      )}
      <style dangerouslySetInnerHTML={{ __html: `
        @keyframes pulse-slow {
          0%, 100% { opacity: 0.8; transform: scale(1); }
          50% { opacity: 1; transform: scale(1.02); }
        }
        .animate-pulse-slow {
          animation: pulse-slow 8s ease-in-out infinite;
        }
      `}} />
    </div>
  );
};

export default App;
