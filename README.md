# Emirati-heritage-in-Arabic-consists-of-more-than-one-category-about-Emirati-customs-and-traditions
Emirati heritage in Arabic consists of more than one category about Emirati customs and traditions
import React, { useState } from "react";
import Header from "./layout/Header";
import CategoryGrid from "./home/CategoryGrid";
import SearchModal from "./search/SearchModal";
import { Sheet, SheetContent, SheetTrigger } from "./ui/sheet";
import { Bookmark } from "lucide-react";

interface Category {
  id: string;
  title: string;
  titleAr: string;
  image: string;
}

interface BookmarkedTradition {
  id: string;
  title: string;
  category: string;
  imageUrl: string;
  description: string;
}

const Home: React.FC = () => {
  const [isSearchOpen, setIsSearchOpen] = useState(false);
  const [isBookmarksOpen, setIsBookmarksOpen] = useState(false);
  const [isMobileMenuOpen, setIsMobileMenuOpen] = useState(false);
  const [selectedCategory, setSelectedCategory] = useState<Category | null>(
    null,
  );

  // Mock bookmarked traditions
  const [bookmarkedTraditions] = useState<BookmarkedTradition[]>([
    {
      id: "1",
      title: "العباية التقليدية",
      category: "الملابس",
      imageUrl:
        "https://images.unsplash.com/photo-1619546952812-520e98064a52?q=80&w=1471&auto=format&fit=crop",
      description:
        "العباية هي رداء تقليدي للنساء الإماراتيات، وهي عبارة عن ثوب طويل وفضفاض يغطي الجسم بالكامل ما عدا الوجه واليدين والقدمين.",
    },
    {
      id: "2",
      title: "القهوة العربية",
      category: "المشروبات",
      imageUrl:
        "https://images.unsplash.com/photo-1578923931302-7a176149fd0f?q=80&w=1470&auto=format&fit=crop",
      description:
        "القهوة العربية هي جزء أساسي من الضيافة الإماراتية التقليدية، وتُقدم في دلة خاصة مع التمر.",
    },
  ]);

  const handleCategorySelect = (category: Category) => {
    setSelectedCategory(category);
    // In a real app, this would navigate to a category detail page
    console.log(`Selected category: ${category.title}`);
  };

  const handleOpenBookmarks = () => {
    setIsBookmarksOpen(true);
  };

  const handleOpenMenu = () => {
    setIsMobileMenuOpen(true);
  };

  return (
    <div className="min-h-screen bg-amber-50 flex flex-col">
      {/* Header */}
      <Header
        onOpenBookmarks={handleOpenBookmarks}
        onOpenMenu={handleOpenMenu}
      />

      {/* Main Content */}
      <main className="flex-1 overflow-auto">
        <CategoryGrid onCategorySelect={handleCategorySelect} />
      </main>

      {/* Search Modal */}
      <SearchModal open={isSearchOpen} onOpenChange={setIsSearchOpen} />

      {/* Bookmarks Sidebar */}
      <Sheet open={isBookmarksOpen} onOpenChange={setIsBookmarksOpen}>
        <SheetContent
          side="right"
          className="w-[350px] sm:w-[450px] bg-amber-50 p-0"
        >
          <div className="h-full flex flex-col">
            <div className="p-6 border-b border-amber-200">
              <h2 className="text-2xl font-bold text-amber-900 text-right">
                العناصر المحفوظة
              </h2>
              <p className="text-amber-700 text-right">Bookmarked traditions</p>
            </div>

            <div className="flex-1 overflow-auto p-4">
              {bookmarkedTraditions.length > 0 ? (
                <div className="space-y-4">
                  {bookmarkedTraditions.map((tradition) => (
                    <div
                      key={tradition.id}
                      className="bg-white rounded-lg shadow-sm p-4 flex gap-3 cursor-pointer hover:shadow-md transition-shadow"
                    >
                      <div className="w-20 h-20 rounded overflow-hidden flex-shrink-0">
                        <img
                          src={tradition.imageUrl}
                          alt={tradition.title}
                          className="w-full h-full object-cover"
                        />
                      </div>
                      <div className="flex-1 text-right">
                        <h3 className="font-bold text-lg text-amber-900">
                          {tradition.title}
                        </h3>
                        <p className="text-sm text-amber-700">
                          {tradition.category}
                        </p>
                        <p className="text-sm text-gray-600 line-clamp-2 mt-1">
                          {tradition.description}
                        </p>
                      </div>
                    </div>
                  ))}
                </div>
              ) : (
                <div className="h-full flex items-center justify-center">
                  <div className="text-center">
                    <Bookmark className="h-12 w-12 text-amber-300 mx-auto mb-4" />
                    <p className="text-amber-900 font-medium">
                      لا توجد عناصر محفوظة
                    </p>
                    <p className="text-amber-700 text-sm">
                      No bookmarked traditions yet
                    </p>
                  </div>
                </div>
              )}
            </div>
          </div>
        </SheetContent>
      </Sheet>

      {/* Mobile Menu */}
      <Sheet open={isMobileMenuOpen} onOpenChange={setIsMobileMenuOpen}>
        <SheetContent side="left" className="w-[300px] bg-amber-50 p-0">
          <div className="h-full flex flex-col">
            <div className="p-6 border-b border-amber-200">
              <h2 className="text-2xl font-bold text-amber-900">القائمة</h2>
              <p className="text-amber-700">Menu</p>
            </div>

            <nav className="flex-1 p-4">
              <ul className="space-y-2">
                <li>
                  <a
                    href="#"
                    className="block p-3 rounded-md hover:bg-amber-100 text-amber-900 font-medium transition-colors"
                  >
                    الصفحة الرئيسية
                  </a>
                </li>
                <li>
                  <a
                    href="#"
                    className="block p-3 rounded-md hover:bg-amber-100 text-amber-900 font-medium transition-colors"
                  >
                    استكشاف الفئات
                  </a>
                </li>
                <li>
                  <a
                    href="#"
                    className="block p-3 rounded-md hover:bg-amber-100 text-amber-900 font-medium transition-colors"
                  >
                    العناصر المحفوظة
                  </a>
                </li>
                <li>
                  <a
                    href="#"
                    className="block p-3 rounded-md hover:bg-amber-100 text-amber-900 font-medium transition-colors"
                  >
                    عن التطبيق
                  </a>
                </li>
              </ul>
            </nav>
          </div>
        </SheetContent>
      </Sheet>
    </div>
  );
};

export default Home;
