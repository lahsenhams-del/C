@tailwind base;
@tailwind components;
@tailwind utilities;

@layer base {
  :root {
    --background: 35 20% 96%;
    --foreground: 0 0% 10%;
    --primary: 348 83% 47%;
    --primary-foreground: 0 0% 100%;
    --secondary: 0 0% 10%;
    --secondary-foreground: 35 20% 96%;
    --accent: 43 74% 66%;
    --japanese-red: 348 83% 47%;
    --dark-bg: 0 0% 10%;
    --cream: 35 20% 96%;
    --gold: 43 74% 66%;
    /* ... المزيد من المتغيرات */
  }

  body {
    @apply bg-background text-foreground font-sans;
    font-family: 'Inter', sans-serif;
  }
  
  h1, h2, h3, h4, h5, h6 {
    font-family: 'Playfair Display', serif;
  }
}
import { motion } from "framer-motion";
import { Button } from "./ui/button";
import { ChevronDown } from "lucide-react";
import heroImage from "@/assets/hero-sushi.jpg";

export const Hero = () => {
  return (
    <section className="relative min-h-screen flex items-center justify-center overflow-hidden">
      <div className="absolute inset-0 z-0">
        <div className="absolute inset-0 bg-cover bg-center" style={{ backgroundImage: `url(${heroImage})` }} />
        <div className="absolute inset-0 bg-gradient-to-b from-dark-bg/80 via-dark-bg/70 to-dark-bg/90" />
      </div>

      {/* Animated Particles */}
      <div className="absolute inset-0 z-10">
        {[...Array(20)].map((_, i) => (
          <motion.div
            key={i}
            className="absolute w-2 h-2 bg-primary/20 rounded-full"
            animate={{
              y: [null, Math.random() * window.innerHeight],
              scale: [0, 1, 0],
              opacity: [0, 1, 0]
            }}
            transition={{
              duration: 3 + Math.random() * 2,
              repeat: Infinity,
              delay: Math.random() * 2
            }}
          />
        ))}
      </div>

      <div className="relative z-20 container mx-auto px-6 text-center">
        <motion.h1 
          className="text-6xl md:text-8xl font-bold text-white mb-6"
          initial={{ opacity: 0, scale: 0.8 }}
          animate={{ opacity: 1, scale: 1 }}
          transition={{ duration: 0.8, delay: 0.2 }}
        >
          Sakura <span className="text-primary">Sushi</span>
        </motion.h1>
        {/* ... المزيد */}
      </div>
    </section>
  );
};
import { motion } from "framer-motion";
import { useInView } from "framer-motion";
import { Button } from "./ui/button";

const menuItems = [
  {
    name: "Nigiri Selection",
    nameAr: "تشكيلة نيجيري",
    description: "تشكيلة فاخرة من السالمون والتونة والجمبري الطازج",
    price: "120",
    image: nigiriImage,
    popular: true
  },
  // ... المزيد
];

export const Menu = () => {
  const ref = useRef(null);
  const isInView = useInView(ref, { once: true, amount: 0.2 });

  return (
    <section ref={ref} className="py-24 bg-white">
      <div className="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
        {menuItems.map((item, index) => (
          <motion.div
            initial={{ opacity: 0, y: 50 }}
            animate={isInView ? { opacity: 1, y: 0 } : {}}
            transition={{ duration: 0.6, delay: index * 0.2 }}
            className="group hover:-translate-y-2"
          >
            {/* ... محتوى الكارد */}
          </motion.div>
        ))}
      </div>
    </section>
  );
};
keyframes: {
  "fade-in": {
    "0%": { opacity: "0", transform: "translateY(20px)" },
    "100%": { opacity: "1", transform: "translateY(0)" }
  },
  "scale-in": {
    "0%": { opacity: "0", transform: "scale(0.9)" },
    "100%": { opacity: "1", transform: "scale(1)" }
  },
  float: {
    "0%, 100%": { transform: "translateY(0)" },
    "50%": { transform: "translateY(-20px)" }
  }
},
animation: {
  "fade-in": "fade-in 0.6s ease-out",
  "scale-in": "scale-in 0.5s ease-out",
  float: "float 3s ease-in-out infinite"
}
import { Hero } from "@/components/Hero";
import { About } from "@/components/About";
import { Menu } from "@/components/Menu";
import { Testimonials } from "@/components/Testimonials";
import { Contact } from "@/components/Contact";
import { Footer } from "@/components/Footer";

const Index = () => {
  return (
    <div className="min-h-screen">
      <Hero />
      <About />
      <Menu />
      <Testimonials />
      <Contact />
      <Footer />
    </div>
  );
};
