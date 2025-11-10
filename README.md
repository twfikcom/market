<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TWFIK - Coming Soon</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;700;900&display=swap" rel="stylesheet">
    
    <!-- Load Babel for in-browser JSX processing -->
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>

    <script>
        window.process = { env: { NODE_ENV: 'production' } };
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                    },
                    colors: {
                        brand: {
                            50: '#f0f9ff',
                            500: '#0ea5e9',
                            600: '#0284c7',
                            900: '#0c4a6e',
                            950: '#082f49',
                        }
                    },
                    animation: {
                        'slow-spin': 'spin 30s linear infinite',
                        'pulse-slow': 'pulse 8s cubic-bezier(0.4, 0, 0.6, 1) infinite',
                        'float': 'float 6s ease-in-out infinite',
                        'lightning': 'lightning 4s ease-in-out infinite',
                    },
                    keyframes: {
                        float: {
                            '0%, 100%': { transform: 'translateY(0px)' },
                            '50%': { transform: 'translateY(-10px)' },
                        },
                        lightning: {
                            '0%, 90%, 100%': { opacity: '1', transform: 'scale(1)', filter: 'brightness(1) drop-shadow(0 0 0 transparent)' },
                            '92%': { opacity: '1', transform: 'scale(1.02)', filter: 'brightness(2) drop-shadow(0 0 5px #0ea5e9)' },
                            '94%': { opacity: '1', transform: 'scale(1)', filter: 'brightness(1) drop-shadow(0 0 0 transparent)' },
                            '96%': { opacity: '1', transform: 'scale(1.02)', filter: 'brightness(2) drop-shadow(0 0 5px #0ea5e9)' },
                        }
                    }
                }
            }
        }
    </script>
    <style>
        body {
            background-color: #000;
            color: #fff;
        }
        .no-scrollbar::-webkit-scrollbar {
            display: none;
        }
        .no-scrollbar {
            -ms-overflow-style: none;
            scrollbar-width: none;
        }
        #root:empty {
           display: none;
        }
        .perspective-container {
            perspective: 2000px;
        }
        .preserve-3d {
            transform-style: preserve-3d;
        }
        .video-background {
            position: fixed;
            right: 0;
            bottom: 0;
            min-width: 100%;
            min-height: 100%;
            width: auto;
            height: auto;
            z-index: -1;
            object-fit: cover;
            opacity: 0.3;
            filter: blur(2px) saturate(0);
        }
        .bg-overlay {
            position: fixed;
            inset: 0;
            z-index: -1;
            background: radial-gradient(circle at center, rgba(14, 165, 233, 0.05) 0%, rgba(0,0,0,0.8) 100%);
            mix-blend-mode: soft-light;
        }
    </style>
</head>
<body class="bg-black text-white antialiased overflow-x-hidden selection:bg-brand-500/30">
    <!-- Real Video Background Placeholder -->
    <video autoplay muted loop playsinline class="video-background">
        <source src="https://assets.mixkit.co/videos/preview/mixkit-abstract-technology-network-connection-lines-27422-large.mp4" type="video/mp4">
    </video>
    <div class="bg-overlay"></div>

    <div id="root"></div>

    <script type="importmap">
    {
      "imports": {
        "react": "https://esm.sh/react@18.2.0",
        "react-dom": "https://esm.sh/react-dom@18.2.0?deps=react@18.2.0",
        "react-dom/client": "https://esm.sh/react-dom@18.2.0/client?deps=react@18.2.0",
        "framer-motion": "https://esm.sh/framer-motion@10.16.16?deps=react@18.2.0,react-dom@18.2.0",
        "lucide-react": "https://esm.sh/lucide-react@0.300.0?deps=react@18.2.0"
      }
    }
    </script>

    <!-- Main Application Logic -->
    <script type="text/babel" data-type="module">
        import React, { useState, useEffect } from 'react';
        import ReactDOM from 'react-dom/client';
        import { motion, AnimatePresence, useSpring, useMotionValue, useTransform } from 'framer-motion';
        import { Loader2, ChevronRight, Mail, Phone } from 'lucide-react';

        const slides = [
            {
                id: 1,
                title: "Redefining Digital Experiences",
                description: "We craft revolutionary platforms that merge creativity with cutting-edge technology.",
            },
            {
                id: 2,
                title: "Next-Gen Performance",
                description: "Engineered for speed, resilience, and seamless scalability to power the future of the web.",
            },
            {
                id: 3,
                title: "Unmatched Security",
                description: "Integrating advanced security protocols to ensure your data remains protected at every level.",
            },
        ];

        const App = () => {
            const [loading, setLoading] = useState(true);
            const [currentSlide, setCurrentSlide] = useState(0);
            const [email, setEmail] = useState("");
            const [notified, setNotified] = useState(false);
            const [sending, setSending] = useState(false);

            const [phone, setPhone] = useState("");
            const [phoneNotified, setPhoneNotified] = useState(false);
            const [phoneSending, setPhoneSending] = useState(false);
            
            const mouseX = useMotionValue(0);
            const mouseY = useMotionValue(0);
            
            const springX = useSpring(mouseX, { damping: 40, stiffness: 300 });
            const springY = useSpring(mouseY, { damping: 40, stiffness: 300 });

            const rotateX = useTransform(springY, [-0.5, 0.5], ["12deg", "-12deg"]);
            const rotateY = useTransform(springX, [-0.5, 0.5], ["-12deg", "12deg"]);

            useEffect(() => {
                const handleMouseMove = (e) => {
                    mouseX.set(e.clientX / window.innerWidth - 0.5);
                    mouseY.set(e.clientY / window.innerHeight - 0.5);
                };
                window.addEventListener("mousemove", handleMouseMove);
                return () => window.removeEventListener("mousemove", handleMouseMove);
            }, []);

            useEffect(() => {
                const timer = setTimeout(() => setLoading(false), 1500);
                return () => clearTimeout(timer);
            }, []);

            useEffect(() => {
                const slideInterval = setInterval(() => {
                    setCurrentSlide((prev) => (prev + 1) % slides.length);
                }, 6000);
                return () => clearInterval(slideInterval);
            }, []);

            const handleSubscribe = async (e) => {
                e.preventDefault();
                if (!email) return;
                setSending(true);
                setTimeout(() => {
                    setNotified(true);
                    setEmail("");
                    setSending(false);
                }, 1500);
            };

            const handlePhoneSubscribe = async (e) => {
                e.preventDefault();
                if (!phone) return;
                setPhoneSending(true);
                setTimeout(() => {
                    setPhoneNotified(true);
                    setPhone("");
                    setPhoneSending(false);
                }, 1500);
            };

            if (loading) {
                return (
                    <div className="fixed inset-0 bg-black flex items-center justify-center overflow-hidden z-50">
                        <motion.div 
                            initial={{ opacity: 0, scale: 0.8 }}
                            animate={{ opacity: 1, scale: 1 }}
                            exit={{ opacity: 0, scale: 1.1 }}
                            transition={{ duration: 0.8, ease: "easeOut" }}
                            className="flex flex-col items-center gap-4"
                        >
                            <motion.div animate={{ rotate: 360 }} transition={{ duration: 2, repeat: Infinity, ease: "linear" }}>
                                <Loader2 className="w-8 h-8 text-brand-500" />
                            </motion.div>
                            <span className="text-sm text-gray-400 tracking-[0.3em] uppercase font-medium">Loading Interface</span>
                        </motion.div>
                    </div>
                );
            }

            const slideVariants = {
                hidden: { opacity: 0, x: 50, filter: 'blur(10px)' },
                visible: { opacity: 1, x: 0, filter: 'blur(0px)', transition: { duration: 0.6, ease: 'circOut' } },
                exit: { opacity: 0, x: -50, filter: 'blur(10px)', transition: { duration: 0.4, ease: 'circIn' } }
            };

            return (
                <div className="min-h-screen relative flex flex-col overflow-hidden">
                    <header className="w-full p-6 md:p-8 flex justify-between items-center relative z-20">
                        <motion.div 
                            initial={{ opacity: 0, y: -20 }}
                            animate={{ opacity: 1, y: 0 }}
                            className="flex items-center space-x-2 group cursor-default"
                        >
                            <div className="w-9 h-9 flex items-center justify-center bg-white/5 rounded-xl border border-white/10 backdrop-blur-md group-hover:border-brand-500/30 transition-colors">
                                <span className="text-xl font-black text-brand-500 animate-lightning">T</span>
                            </div>
                            <span className="text-lg font-bold tracking-wider text-white">TWFIK<span className="text-brand-500">.</span></span>
                        </motion.div>
                        <div className="px-3 py-1.5 rounded-full bg-white/5 border border-white/10 backdrop-blur-md text-xs font-medium flex items-center gap-2">
                            <span className="flex h-1.5 w-1.5 relative">
                                <span className="animate-ping absolute inline-flex h-full w-full rounded-full bg-brand-400 opacity-75"></span>
                                <span className="relative inline-flex rounded-full h-1.5 w-1.5 bg-brand-500"></span>
                            </span>
                            <span className="text-gray-300 tracking-wider uppercase">Beta</span>
                        </div>
                    </header>

                    <main className="flex-1 flex flex-col items-center justify-center px-4 relative z-20 text-center py-8 perspective-container">
                        <motion.div
                            initial={{ opacity: 0, y: 30 }}
                            animate={{ opacity: 1, y: 0 }}
                            transition={{ duration: 1 }}
                            className="mb-12"
                        >
                            <h1 className="text-5xl md:text-7xl font-black tracking-tighter mb-6 bg-clip-text text-transparent bg-gradient-to-b from-white to-white/60 leading-[1.1] drop-shadow-2xl animate-lightning">
                                FUTURE IS<br />
                                <span className="text-white">COMING SOON</span>
                            </h1>
                            <p className="text-lg text-gray-400 max-w-xl mx-auto leading-relaxed">
                                Prepare for a new era of digital innovation by <span className="text-white font-semibold">TWFIK</span>.
                            </p>
                        </motion.div>

                        <motion.div 
                            style={{ rotateX, rotateY, transformStyle: "preserve-3d" }}
                            className="w-full max-w-4xl h-auto min-h-[240px] relative"
                        >
                            <AnimatePresence mode="wait">
                                <motion.div
                                    key={currentSlide}
                                    variants={slideVariants}
                                    initial="hidden"
                                    animate="visible"
                                    exit="exit"
                                    className="absolute inset-0 flex flex-col items-center md:items-start p-8 rounded-3xl bg-black/40 border border-white/10 backdrop-blur-2xl text-center md:text-left shadow-2xl"
                                >
                                    <div className="flex-1 p-2">
                                        <h2 className="text-xl font-bold mb-3 text-white">{slides[currentSlide].title}</h2>
                                        <p className="text-gray-400 leading-relaxed">{slides[currentSlide].description}</p>
                                    </div>
                                </motion.div>
                            </AnimatePresence>
                            
                            {/* Indicators */}
                            <div className="absolute -bottom-16 left-1/2 -translate-x-1/2 flex gap-2">
                                {slides.map((_, index) => (
                                    <div key={index} className={`h-1 rounded-full transition-all duration-500 ${index === currentSlide ? 'w-8 bg-brand-500' : 'w-2 bg-white/20'}`} />
                                ))}
                            </div>
                        </motion.div>

                        <div className="mt-24 w-full max-w-md flex flex-col gap-4">
                            {/* Email Form */}
                            <div className="bg-black/60 backdrop-blur-xl rounded-full p-1.5 border border-white/10 flex items-center transition-colors focus-within:border-white/30">
                                <Mail className="w-5 h-5 ml-3 mr-2 text-gray-500" />
                                <input 
                                    type="email" 
                                    value={email}
                                    onChange={(e) => setEmail(e.target.value)}
                                    placeholder="Enter your email address"
                                    className="flex-1 bg-transparent text-sm text-white placeholder:text-gray-500 outline-none"
                                    disabled={sending || notified}
                                />
                                <button 
                                    onClick={handleSubscribe}
                                    disabled={sending || notified}
                                    className="bg-white text-black px-4 py-2 rounded-full text-sm font-semibold hover:bg-gray-100 transition-colors disabled:opacity-50"
                                >
                                    {sending ? <Loader2 className="w-4 h-4 animate-spin" /> : notified ? "Subscribed" : "Notify Me"}
                                </button>
                            </div>

                            {/* Phone Form */}
                            <div className="bg-black/60 backdrop-blur-xl rounded-full p-1.5 border border-white/10 flex items-center transition-colors focus-within:border-white/30">
                                <Phone className="w-5 h-5 ml-3 mr-2 text-gray-500" />
                                <input 
                                    type="tel" 
                                    value={phone}
                                    onChange={(e) => setPhone(e.target.value)}
                                    placeholder="Enter phone number for SMS"
                                    className="flex-1 bg-transparent text-sm text-white placeholder:text-gray-500 outline-none"
                                    disabled={phoneSending || phoneNotified}
                                />
                                <button 
                                    onClick={handlePhoneSubscribe}
                                    disabled={phoneSending || phoneNotified}
                                    className="bg-white/10 text-white px-4 py-2 rounded-full text-sm font-semibold hover:bg-white/20 transition-colors disabled:opacity-50"
                                >
                                    {phoneSending ? <Loader2 className="w-4 h-4 animate-spin" /> : phoneNotified ? "Subscribed" : "Send SMS"}
                                </button>
                            </div>
                        </div>
                    </main>

                    <footer className="py-6 text-center text-gray-500 text-sm border-t border-white/5 relative z-20">
                        © {new Date().getFullYear()} TWFIK. All rights reserved.
                    </footer>
                </div>
            );
        };

        const root = ReactDOM.createRoot(document.getElementById('root'));
        root.render(<App />);
    </script>
</body>
</html>
