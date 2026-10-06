import { useEffect, useState } from "react";
import Icon from "@/components/ui/icon";
import { DiscordIcon, TelegramIcon, LINKS } from "./SocialIcons";

const NAV = [
  { href: "#top", label: "Главная" },
  { href: "#roster", label: "Состав" },
  { href: "#matches", label: "Матчи" },
  { href: "#join", label: "Вступить в команду" },
  { href: "#contacts", label: "Контакты" },
];

export const Brand = () => (
  <a
    href="#top"
    aria-label="Govu1sen — на главную"
    className="flex items-center gap-[9px] font-head text-[1.6em] font-extrabold tracking-[-0.03em] text-foreground"
  >
    <span aria-hidden="true" className="h-[18px] w-[30px] rounded-[12px_12px_4px_4px] bg-primary" />
    <span>
      govu<b className="font-extrabold text-primary">1</b>sen
    </span>
  </a>
);

const VDiv = () => <span aria-hidden="true" className="mx-[30px] h-8 w-0 border-l border-dotted border-muted-foreground" />;

const Header = () => {
  const [open, setOpen] = useState(false);
  const [scrolled, setScrolled] = useState(false);

  useEffect(() => {
    const onScroll = () => setScrolled(window.scrollY > 8);
    onScroll();
    window.addEventListener("scroll", onScroll, { passive: true });
    return () => window.removeEventListener("scroll", onScroll);
  }, []);

  useEffect(() => {
    const onKey = (e: KeyboardEvent) => e.key === "Escape" && setOpen(false);
    window.addEventListener("keydown", onKey);
    return () => window.removeEventListener("keydown", onKey);
  }, []);

  return (
    <header
      className={`fixed inset-x-50 transition-colors duration-300 ${
        scrolled || open ? "bg-background/90 backdrop-blur-md border-b border-dashed border-border" : "bg-background"
      }`}
    >
      <div className="mx-auto flex h-[76px] max-w-[1440px] items-center px-5 md:px-8 lg:h-[88px] lg:px-11">
        <Brand />
        <span className="hidden lg:block">
          <VDiv />
        </span>
        <nav aria-label="Основное меню" className="hidden gap-[26px] text-[0.94em] font-medium lg:flex">
          {NAV.filter((n) => n.href !== "#join").map((n) => (
            <a key={n.href} href={n.href} className="transition-colors hover:text-primary">
              {n.label}
            </a>
          ))}
        </nav>

        <div className="ml-auto hidden items-center lg:flex">
          <div className="flex gap-[22px]">
            {/* Замени ссылки на Discord и Telegram в файле с контактами */}
            <a href={LINKS.discord} aria-label="Discord" className="transition-colors hover:text-primary">
              <DiscordIcon className="h-[22px] w-[22px]" />
            </a>
            <a href={LINKS.telegram} aria-label="Telegram" className="transition-colors hover:text-primary">
              <TelegramIcon className="h-[22px] w-[22px]" />
            </a>
          </div>
          <VDiv />
          <a href="#join" className="pill pill-fill h-[46px] px-6 text-[0.94em]">
            Вступить в команду
          </a>
        </div>

        <button
          type="button"
          className="ml-auto flex h-11 w-11 items-center justify-center rounded-fullforeground transition-colors hover:border-primary hover:text-primary lgria-label={open ? "Закрыть меню" : "Открыть меню"}
          aria-expanded={open}
          aria-controls="mobile-menu"
          onClick={() => setOpen((v) => !v)}
        >
          <Icon name={open ? "X" : "Menu"} size={22} />
        </button>
      </div>

      {open && (
        <nav id="mobile-menu" aria-label="Мобильное меню" className="animate-fade-in border-t border-dashed border-border px-5 pb-6 pt-2 md:px-8 lg:hidden">
          <ul className="flex flex-col">
            {NAV.map((n) => (
              <li key={n.href}>
                <a
                  href={n.href}
                  onClick={() => setOpen(false)}
                  className="flex items-center justify-between border-b border-dashed border-border py-4 font-head text-2xl font-extrabold tracking-tight transition-colors hover:text-primary"
                >
                  {n.label}
                  <Icon name="ArrowUpRight" size={20} className="text-muted-foreground" />
                </a>
              </li>
            ))}
          </ul>
          <div className="mt-5 flex gap-3">
            <a href={LINKS.discord} aria-label="Discord" className="pill pill-ghost h-11 w-11">
              <DiscordIcon className="h-5 w-5" />
            </a>
            <a href={LINKS.telegram} aria-label="Telegram" className="pill pill-ghost h-11 w-11">
              <TelegramIcon className="h-5 w-5" />
            </a>
          </div>
        </nav>
      )}
    </header>
  );
};

export default Header;
import Icon from "@/components/ui/icon";
import SectionHead from "./SectionHead";

const FACTS = [
  { icon: "MapPin", title: "Из Санкт-Петербурга", text: "Базируемся в Питере, тренируемся вместе и выезжаем на LAN-турниры." },
  { icon: "GraduationCap", title: "Представляем НУЦ", text: "Играем под флагом НУЦ и защищаем его имя на каждом матче." },
  { icon: "Crosshair", title: "Тренируемся на FastCup", text: "Регулярные тренировки на FastCup, разборы игр и участие в онлайн- и офлайн-турнирах." },
];

// Замени цифры на реальные показатели команды
const STATS = [
  { value: "1–10", label: "любой уровень Faceit" },
  { value: "4×", label: "тренировки в неделю" },
  { value: "12+", label: "турниров за сезон" },
];

const About = () => (
  <section id="about" className="mx-auto max-w-[1440px] px-5 py-16 md:px-8 lg:px-11 lg:py-24">
    <SectionHead
      index="01"
      kicker="О команде"
      title={
        <>
          Играем в серьёзный CS <span className="text-primary">и делаем это системно</span>
        </>
      }
    />

    <div className="grid gap-4 lg:grid-cols-12">
      <div className="rounded-tile border border-dashed border-border bg-card p-7 lg:col-span-7 lg:p-10">
        <p className="text-lg leading-relaxed md:text-xl">
          Govu1sen — команда из Санкт-Петербурга, которая представляет НУЦ в Counter-Strike 2.
          <span className="text-muted-foreground">
            {" "}
            Мы собрались, чтобы играть на конкурентном уровне: тренируемся на FastCup по расписанию и регулярно
            выходим на турниры. Разбираем демки, строим тактикичу — без громких
            слов, с результатом на табло.
          </span>
        </p>
      </div>
      <div className="grid grid-cols-3 gap-4 lg:col-span-5">
        {STATS.map((s) => (
          <div key={s.label} className="tile-hover flex flex-col justify-between rounded-tile border border-dashed border-border bg-card p-5 lg:p-6">
            <div className="font-head text-4xl font-black tracking-tight text-primary lg:text-5xl">{s.value}</div>
            <div className="mt-6 text-sm text-muted-foreground">{s.label}</div>
          </div>
        ))}
      </div>

      {FACTS.map((f) => (
        <article key={f.title} className="tile-hover rounded-tile border border-dashed border-border bg-card p-7 lg:col-span-4">
          <div className="mb-10 flex h-12 w-12 items-center justify-center rounded-full bg-primary text-primary-foreground">
            <Icon name={f.icon} size={22} />
          </div>
          <h3 className="mb-2 font-head text-2xl font-extrabold tracking-tight">{f.title}</h3>
          <p className="text-muted-foreground">{f.text}</p>
        </article>
      ))}
    </div>
  </section>
);

export default About;
const Hero = () => {
  return (
    <section
      id="top"
      className="mx-auto grid max-w-[1440px] gap-4 px-5 pb-8 pt-[92px] md:px-8 lg:h-screen lg:min-h-[680px] lg:max-h-[860px] lg:grid-cols-[548px_1fr] lg:gap-0 lg:px-11 lg:pb-10 lg:pt-[100px]"
    >
      {/* Текст */}
      <div className="flex flex-col justify-between gap-8 lg:pr-9 lg:pt-[22px]">
        <h1 className="animate-fade-in font-head text-[40px] font-black leading-[0.98] tracking-[-0.035em] sm:text-[48px] lg:text-[54px]">
          Govu<span className="text-primary">1</span>sen — киберспортивная команда из Санкт&#8209;Петербурга
        </h1>
        <div className="animate-fade-in rounded-tile bg-card p-6 [animation-delay:150ms] sm:p-[30px]">
          <p className="mb-[26px] max-w-[440px] text-[1.06em] leading-[1.55]">
            Представляем НУЦ. Играем в CS на конкурентном уровне — тренируемся, побеждаем, растём.{" "}
            <span className="text-muted-foreground">Ищем игроков, которые готовы к серьёзному формату.</span>
          </p>
          <div className="flex flex-col gap-3.5 sm:flex-row">
            <a href="#join" className="pill pill-fill h-[54px] px-[30px] text-[1.06em] sm:min-w-[214px]">
              Вступить в команду
            </a>
            <a href="#matches" className="pill pill-ghost h-[54px] px-[30px] text-[1.06em] sm:min-w-[214px]">
              Смотреть матчи
            </a>
          </div>
        </div>
      </div> с логотипом */}
      <figure
        aria-label="Логотип Govu1sen"
        className="animate-scale-in relative aspect-square overflow-hidden rounded-tile bg-halftone [animation-delay:250ms] sm:aspect-[4/3] lg:aspect-auto"
      >
        <div className="ht ht-1" />
        <div className="ht ht-2" />
        <div className="ht ht-3" />
        <div className="ht ht-solid" />
        <div className="ht ht-4" />
        <div
          aria-hidden="true"
          className="absolute inset-x-6 top-1/2 -translate-y-1/2 font-head text-[27vw] font-black uppercase leading-[0.84] tracking-[-0.055em] text-background sm:inset-x-11 sm:text-[20vw] lg:text-[clamp(px)] xl:text-[127px]"
        >
          <span className="block">Govu</span>
          <span className="block text-right">1sen</span>
        </div>
        <div className="absolute bottom-[26px] left-7 rounded-full bg-background px-[18px] py-2.5 text-[0.88em] font-medium text-foreground">
          CS2 <i className="not-italic text-muted-foreground">·</i> НУЦ <i className="not-italic text-muted-foreground">·</i> СПб
        </div>
      </figure>
    </section>
  );
};

export default Hero;
// Замени ник и роль игроков; когда появятся аватарки — подставь их вместо буквы
const PLAYERS = [
  { nick: "ka1zen", role: "IGL" },
  { nick: "zimoro_4", role: "Rifler" },
];

const Roster = () => (
  <section id="roster" className="mx-auto max-w-[1440px] px-5 py-16 md:px-8 lg:px-11 lg:py-24">
    <h2 className="mb-12 text-center font-head text-4xl font-black uppercase tracking-[0.08em] text-white md:text-6xl">
      Наша команда
    </h2>

    <div className="mx-auto grid max-w-3xl gap-6 sm:grid-cols-2">
      {PLAYERS.map((p) => (
        <article
          key={p.nick}
          tabIndex={0}
          className="flex flex-col items-center rounded-tile border border-white/15 bg-black/40 px-6 py-10 text-center backdrop-blur-sm transition-all duration-300 hover:-translate-y-2 hover:border-primary/50 hover:shadow-[0_12px_40px_-8px_rgba(0,229,255,0.45)] focus-visible:-translate-y-2 focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-primary"
        >
          <div
            aria-hidden="true"
            className="mb-6 flex h-24 w-24 items-center justify-center rounded-full bg-neutral-600 font-head text-5xl font-black text-white"
          >
            {p.nick[0].toUpperCase()}
          </div>
          <h3 className="font-head text-3xl font-black tracking-tight text-white">{p.nick}</h3>
          <p className="mt-2 text-sm font-semibold uppercase tracking-wider text-primary">{p.role}</p>
        </article>
      ))}
    </div>
  </section>
);

export default Roster;
import { Tabs, TabsContent, TabsList, TabsTrigger } from "@/components/ui/tabs";
import Icon from "@/components/ui/icon";
import SectionHead from "./SectionHead";

type Status = "Ожидается" | "Подтверждено";

// Замени даты, турниры, соперников и ссылки на стрим
const UPCOMING: { date: string; tournament: string; opponent: string; format: string; status: Status; stream: string }[] = [];

// Замени на реальные сыгранные матчи и ссылки на демо
const PLAYED: { date: string; tournament: string; opponent: string; score: string; result: "W" | "L"; demo: string }[] = [];

// Замени на полный список матчей
const ALL: { date: string; tournament: string; opponent: string; score: string; format: string; result: string }[] = [
  { date: "07.10.2026", tournament: "Турнир FastCup · $20", opponent: "—", score: "—", format: "—", result: "Сорван" },
];

const Empty = () => (
  <tr className="border-t border-dashed border-border">
    <td colSpan={6} className="px-5 py-10 text-center text-muted-foreground">
      Матчи не предстоят
    </td>
  </tr>
);

const th = "whitespace-nowrap px-5 py-4 text-left text-xs font-semibold uppercase tracking-wider text-muted-foreground";
const td = "whitespace-nowrap px-5 py-4";
const row = "border-t border-dashed border-border transition-colors hover:bg-secondary/60";

const Result = ({ r }: { r: string }) =>
  r !== "W" && r !== "L" ? (
    <span className={r === "—" ? "text-muted-foreground" : "inline-flex rounded-full border border-dotted border-destructive px-3 py-1 text-sm font-medium text-destructive"}>
      {r}
    </span>
  ) : (
    <span
      className={`inline-flex h-8 w-8 items-center justify-center rounded-full font-head font-black ${
        r === "W" ? "bg-success text-success-foreground" : "bg-destructive text-destructive-foreground"
      }`}
      aria-label={r === "W" ? "Победа" : "Поражение"}
    >
      {r}
    </span>
  );

const TableWrap = ({ children, label }: { children: React.ReactNode; label: string }) => (
  <div className="overflow-x-auto rounded-tile border border-dashed border-border bg-card" tabIndex={0} role="region" aria-label={label}>
    <table className="w-full min-w-[720px] border-collapse">{children}</table>
  </div>
);

const trigger =
  "rounded-full px-5 py-2.5 text-sm font-medium text-muted-foreground transition-all hover:text-foreground data-[state=active]:bg-primary data-[state=active]:text-primary-foreground data-[state=active]:shadow-none";

const Matches = () => {
  const wins = PLAYED.filter((m) => m.result === "W").length;
  return (
    <section id="matches" className="mx-auto max-w-[1440px] px-5 py-16 md:px-8 lg:px-11 lg:py-24">
      <SectionHead
        index="03"
        kicker="Матчи"
        title={
          <>
            Расписание <span className="text-primary">и результаты</span>
          </>
        }
        text={
          PLAYED.length ? (
            <>
              Последние матчи: <span className="font-semibold text-success">{wins} W</span> /{" "}
              <span className="font-semibold text-destructive">{PLAYED.length - wins} L</span>. Следи за ближайшими играми и
              смотри трансляции.
            </>
          ) : (
            "Следи за ближайшими играми и смотри трансляции."
          )
        }
      />

      <Tabs defaultValue="upcoming">
        <TabsList className="to flex-wrap justify-start gap-1 rounded-full border border-dotted border-border bg-card p-1.5">
          <TabsTrigger value="upcoming" className={trigger}>
            Предстоящие
          </TabsTrigger>
          <TabsTrigger value="played" className={trigger}>
            Сыгранные
          </TabsTrigger>
          <TabsTrigger value="all" className={trigger}>
            Все матчи
          </TabsTrigger>
        </TabsList>

        <TabsContent value="upcoming" className="animate-fade-in">
          <TableWrap label="Предстоящие матчи">
            <thead>
              <tr>
                <th className={th}>Дата</th>
                <th className={th}>Турнир</th>
                <th className={th}>Соперник</th>
                <th className={th}>Формат</th>
                <th className={th}>Статус</th>
                <th className={th}>
                  <span className="sr-only">Трансляция</span>
                </th>
              </tr>
            </thead>
            <tbody>
              {UPCOMING.length === 0 && <Empty />}
              {UPCOMING.map((m, i) => (
                <tr key={i} className={row}>
                  <td className={`${td} font-medium`}>{m.date}</td>
                  <td className={`${td} text-muted-foreground`}>{m.tournament}</td>
                  <td className={`${td} font-head text-lg font-extrabold`}>td>
                  <td className={td}>
                    <span className="rounded-full border border-dotted border-foreground px-3 py-1 text-sm">{m.format}</span>
                  </td>
                  <td className={td}>
                    <span
                      className={`inline-flex items-center gap-2 text-sm font-medium ${
                        m.status === "Подтверждено" ? "text-primary" : "text-muted-foreground"
                      }`}
                    >
                      <span className={`h-2 w-2 rounded-full ${m.status === "Подтверждено" ? "bg-primary" : "bg-muted-foreground"}`} />
                      {m.status}
                    </span>
                  </td>
                  <td className={`${td} text-right`}>
                    {/* Замени ссылку на стрим */}
                    <a href={m.stream} className="pill pill-fill h-10 px-5 text-sm">
                      <Icon name="Play" size={14} />
                      Смотреть
                    </a>
                  </td>
                </tr>
              ))}
            </tbody>
          </TableWrap>
        </TabsContent>

        <TabsContent value="played" className="animate-fade-in">
          <TableWrap label="Сыгранные матчи">
            <thead>
              <tr>
                <th className={th}>Дата</th>
                <th className={th}>Турнир</th>
                <th className={th}>Соперник</th>
                <th className={th}>Счёт</th>
                <th className={th}>Результат</th>
                <th className={th}>
                  <span className="sr-only">Демо</span>
                </th>
              </tr>
            </thead>
            <tbody>
              {PLAYED.length === 0 && <Empty />}
              {PLAYED.map((m, i) => (
                <tr key={i} className={row}>
                  <td className={`${td} font-medium`}>{m.date}</td>
                  <td className={`${td} text-muted-foreground`}>{m.tournament}</td>
                  <td className={`${td} font-head text-lg font-extrabold`}>{m.opponent}</td>
                  <td className={`${td} font-head text-lg font-extrabold`}>{m.score}</td>
                  <td className={td}>
                    <Result r={m.result} />
                  </td>
                  <td className={`${td} text-right`}>
                    {/* Замени ссылку на демо */}
                    <a href={m.demo} className="pill pill-ghost h-10 px-5 text-sm">
                      <Icon name="Download" size={14} />
                      Демо
                    </a>
                  </td>
                </tr>
              ))}
            </tbody>
          </TableWrap>
        </TababsContent value="all" className="animate-fade-in">
          <TableWrap label="Все матчи">
            <thead>
              <tr>
                <th className={th}>Дата</th>
                <th className={th}>Турнир</th>
                <th className={th}>Соперник</th>
                <th className={th}>Счёт</th>
                <th className={th}>Формат</th>
                <th className={th}>Результат</th>
              </tr>
            </thead>
            <tbody>
              {ALL.length === 0 && <Empty />}
              {ALL.map((m, i) => (
                <tr key={i} className={row}>
                  <td className={`${td} font-medium`}>{m.date}</td>
                  <td className={`${td} text-muted-foreground`}>{m.tournament}</td>
                  <td className={`${td} font-head text-lg font-extrabold`}>{m.opponent}</td>
                  <td className={`${td} font-head text-lg font-extrabold`}>{m.score}</td>
                  <td className={td}>
                    <span className="rounded-full border border-dotted border-foreground px-3 py-1 text-sm">{m  </td>
                  <td className={td}>
                    <Result r={m.result} />
                  </td>
                </tr>
              ))}
            </tbody>
          </TableWrap>
        </TabsContent>
      </Tabs>
      <p className="mt-3 text-sm text-muted-foreground md:hidden">Таблицу можно прокрутить вбок.</p>
    </section>
  );
};

export default Matches;
import { useState } from "react";
import Icon from "@/components/ui/icon";
import SectionHead from "./SectionHead";

type Errors = Partial<Record<"nick" | "age" | "contact" | "profile", string>>;

const FORMSPREE_URL = "https://formspree.io/f/meaolrwy";

const ROLES = ["IGL", "AWP", "Rifler", "Support", "Entry", "Lux"];

const Label = ({ htmlFor, children, required }: { htmlFor: string; children: React.ReactNode; required?: boolean }) => (
  <label htmlFor={htmlFor} className="mb-2 block text-sm font-medium">
    {children}
    {required && <span className="ml-1 text-primary">*</span>}
  </label>
);, text }: { id: string; text?: string }) =>
  text ? (
    <p id={id} className="mt-1.5 text-sm text-destructive">
      {text}
    </p>
  ) : null;

const JoinForm = () => {
  const [errors, setErrors] = useState<Errors>({});
  const [sent, setSent] = useState(false);
  const [sending, setSending] = useState(false);
  const [sendError, setSendError] = useState("");

  const onSubmit = async (e: React.FormEvent<HTMLFormElement>) => {
    e.preventDefault();
    const form = e.currentTarget;
    const fd = new FormData(form);
    const next: Errors = {};
    const nick = String(fd.get("nick") || "").trim();
    const age = String(fd.get("age") || "");
    const contact = String(fd.get("contact") || "").trim();
    const profile = String(fd.get("profile") || "").trim();
    if (!nick) next.nick = "Укажи свой игровой ник";
    if (age && Number(age) < 14) next.age = "Принимаем игроков от 14 лет";
    if (!contact) next.contact = "Оставь Telegram или Discord для связи";
    if (profile && !/^https?:\/\/.+\..+/.test(profile)) next.profile = "Ссылка должна начинаться с https://";
    setErrors(next);
    if (Object.keys(next).length) return;
    fd.set("ready", fd.get("ready") ? "Да" : "Нет");
    fd.set("_subject", `Заявка в Govu1sen от ${nick}`);
    setSendError("");
    setSending(true);
    try {
      const res = await fetch(FORMSPREE_URL, { method: "POST", body: fd, headers: { Accept: "application/json" } });
      if (!res.ok) throw new Error();
      setSent(true);
      form.reset();
    } catch {
      setSendError("Не удалось отправить заявку. Попробуй ещё раз или напиши нам в Telegram.");
    } finally {
      setSending(false);
    }
  };

  return (
    <section id="join" className="mx-auto max-w-[1440px] px-5 py-16 md:px-8 lg:px-11 lg:py-24">
      <SectionHead
        index="04"
        kicker="Вступить в команду"
        title={
          <>
            Хочешь в <span className="text-primary">Govu1sen?</span>
          </>
        }
        text="Мы ищем игроков из Санкт-Петербурга и не только. Опыт в CS, адекватность, готовность тренироваться и играть в турнирах — обязательно."
      />

      <div className="grid gap-4 lg:grid-cols-12">
        <aside className="relative overflow-hidden rounded-tile bg-halftone p-7 text-background lg:col-span-4 lg:p-9">
          <div className="ht ht-1" />
          <div className="ht <div className="relative">
            <h3 className="mb-6 font-head text-3xl font-black leading-tight tracking-tight">Что мы ждём</h3>
            <ul className="space-y-3">
              {["Любой уровень Faceit", "Тренировки на FastCup 3+ раза в неделю", "Микрофон и адекватная коммуникация", "Готовность к турнирам и разборам демо"].map((t) => (
                <li key={t} className="flex items-start gap-3 rounded-2xl bg-background px-4 py-3 text-sm font-medium text-foreground">
                  <Icon name="Check" size={18} className="mt-0.5 shrink-0 text-primary" />
                  {t}
                </li>
              ))}
            </ul>
          </div>
        </aside>

        <div className="rounded-tile border border-dashed border-border bg-card p-6 sm:p-8 lg:col-span-8 lg:p-10">
          {sent ? (
            <div className="flex min-h-[420px] animate-scale-in flex-col items-center justify-center text-center" role="status">
              <div className="mb-6 flex h-16 w-16 items-center justify-center rounded-full bg-primary text-primary-foreground">
                <Icon name="Check" size={30} />
              </div>
              <h3 className="mb-3 font-head text-3xl font-black tracking-tight">Заявка принята</h3>
              <p className="mb-8 max-w-md text-muted-foreground">
                Спасибо! Мы посмотрим твой профиль и напишем в указанный контакт в течение нескольких дней.
              </p>
              <button type="button" onClick={() => setSent(false)} className="pill pill-ghost h-12 px-6">
                Отправить ещё одну
              </button>
            </div>
          ) : (
            <form action={FORMSPREE_URL} method="POST" noValidate onSubmit={onSubmit} className="grid gap-5 sm:grid-cols-2">
              <div>
                <Label htmlFor="nick" required>Ник</Label>
                <input id="nick" name="nick" type="text" required className="field" placeholder="Твой игровой ник" aria-invalid={!!errors.nick} aria-describedby="nick-err" />
                <Err id="nick-err" text={errors.nick} />
              </div>
              <div>
                <Label htmlFor="age">Возраст</Label>
                <input id="age" name="age" type="number" min={14} className="field" placeholder="от 14" aria-invalid={!!errors.age} aria-describedby="age-err" />
                <Err id="age-err" text={errors.age} />
              </div>
              <div>
                <Label htmlFor="city">Город</Label>
                <input id="city" name="city" type="text" className="field" placeholder="Санкт-Петербург" />
              </div>
              <div>
                <Label htmlFor="faceit">Faceit уровень</Label>
                <select id="faceit" name="faceit" className="field appearance-none" defaultValue="">
                  <option value="" disabled>Выбери уровень</option>
                  {Array.from({ length: 10 }, (_, i) => i + 1).map((l) => (
                    <option key={l} value={l}>{l}</option>
                  ))}
                </select>
              </div>
              <div>
                <Label htmlFor="hours">Часы в CS</Label>
                <input id="hours" name="hours" type="number" min={0} className="field" placeholder="Например, 3000" />
              </div>
              <div>
                <Label htmlFor="role">Роль</Label>
                <select id="role" name="role" className="field appearance-none" defaultValue="">
                  <option value="" disabled>Выбери роль</option>
                  {ROLES.map((r) => (
                    <option key={r} value={r}>{r}</option>
                  ))}
                </select>
              </div>
              <div className="sm:col-span-2">
                <Label htmlFor="experience">Опыт в турнирах</Label>
                <textarea id="experience" name="experience" rows={4} className="field resize-y" placeholder="В каких турнирах играл, с какими командами, лучшие результаты" />
              </div>
              <div>
                <Label htmlFor="profile">Ссылка на профиль Faceit/Steam</Label>
                <input id="profile" name="profile" type="url" className="field" placeholder="https://faceit.com/..." aria-invalid={!!errors.profile} aria-describedby="profile-err" />
                <Err id="profile-err" text={errors.profile} />
              </div>
              <div>
                <Label htmlFor="contact" required>Контакт (Telegram/Discord)</Label>
                <input id="contact" name="contact" type="text" required className="field" placeholder="@username" aria-invalid={!!errors.contact} aria-describedby="contact-err" />
                <Err id="contact-err" text={errors.contact} />
              </div>
              <label htmlFor="ready" className="flex cursor-pointer items-center gap-3 sm:col-span-2">
                <input id="ready" name="ready" type="checkbox" className="peer h-5 w-5 shrink-0 cursor-pointer
                <span className="text-sm">Готов к тренировкам 3+ раза в неделю</span>
              </label>
              <div className="flex flex-col items-start gap-3 sm:col-span-2 sm:flex-row sm:items-center sm:justify-between">
                <p className="text-sm text-muted-foreground">
                  Поля со звёздочкой <span className="text-primary">*</span> обязательны
                </p>
                <button type="submit" disabled={sending} className="pill pill-fill h-[54px] w-full px-[30px] text-[1.06em] disabled:opacity-60 sm:w-auto sm:min-w-[214px]">
                  {sending ? "Отправляем..." : "Отправить заявку"}
                  <Icon name={sending ? "Loader2" : "ArrowRight"} size={18} className={sending ? "animate-spin" : ""} />
                </button>
              </div>
              {sendError && (
                <p role="alert" className="text-sm text-destructive sm:col-span-2">
                  {sendError}
                </p>
              )}
            </form>
          )}
        </div>
      </div>
    </section>
  );
};

export default JoinForm;
import SectionHead from "./SectionHead";
import { Brand } from "./Header";
import { LINKS } from "./SocialIcons";

// Замени контакты на реальные
const CONTACTS = [
  { emoji: "🎮", label: "Discord", value: "discord.gg/govu1sen", href: LINKS.discord },
  { emoji: "✈️", label: "Telegram", value: "@govu1sen", href: LINKS.telegram },
  { emoji: "✉️", label: "Почта", value: LINKS.email, href: `mailto:${LINKS.email}` },
];

const Footer = () => (
  <footer id="contacts" className="mx-auto max-w-[1440px] px-5 pb-8 pt-16 md:px-8 lg:px-11 lg:pt-24">
    <SectionHead
      index="05"
      kicker="Контакты"
      title={
        <>
          На связи <span className="text-primary">каждый день</span>
        </>
      }
      text="По вопросам сотрудничества, турниров и праков — пиши в любой удобный канал."
    />

    <div className="grid gap-4 md:grid-cols-3">
      {CONTACTS.map((c) => (
        <a
          key={c.label}
          href={c.href}
          className="tile-hover group flex items-center gap-5 rounded-tile border border-dashed border-border bg-card p-6"
        >
          <span aria-hidden="true" className="flex h-14 w-14 shrink-0 items-center justify-center rounded-full bg-background text-2xl">
            {c.emoji}
          </span>
          <span className="min-w-0">
            <span className="block text-sm text-muted-foreground">{c.label}</span>
            <span className="block truncate font-head text-xl font-extrabold tracking-tight transition-colors group-hover:text-primary">
              {c.value}
            </span>
          </span>
        </a>
      ))}
    </div>

    <div className="mt-16 flex flex-col gap-6 border-t border-dashed border-border pt-8 md:flex-row md:items-center md:justify-between">
      <Brand />
      <p className="text-sm text-muted-foreground md:text-center">
        Команда представляет НУЦ в студенческом и открытом киберспорте.
      </p>
      <p className="text-sm text-muted-foreground">© 2026 Govu1sen. Санкт-Петербург.</p>
    </div>
  </footer>
);

export default Footer;
interface Props {
  index: string;
  kicker: string;
  title: React.ReactNode;
  text?: React.ReactNode;
}

const SectionHead = ({ index, kicker, title, text }: Props) => (
  <div className="mb-8 grid gap-4 md:mb-10 md:grid-cols-[1fr_minmax(0,420px)] md:items-end">
    <div>
      <div className="mb-4 flex items-center gap-3 text-sm font-medium text-muted-foreground">
        <span className="rounded-full border border-dotted border-primary px-3 py-1 text-primary">{index}</span>
        {kicker}
      </div>
      <h2 className="font-head text-[36px] font-black leading-[0.98] tracking-[-0.035em] sm:text-[44px] lg:text-[54px]">{title}</h2>
    </div>
    {text && <p className="leading-relaxed text-muted-foreground">{text}</p>}
  </div>
);

export default SectionHead;
export const DiscordIcon = ({ className = "" }: { className?: string }) => (
  <svg viewBox="0 0 24 24" className={className} fill="currentColor" aria-hidden="true">
    <path d="M19.6 5.3A17 17 0 0 0 15.4 4l-.5 1.1a15.7 15.7 0 0 0-5.8 0L8.6 4a17 17 0 0 0-4.2 1.3C1.7 9.3 1 13.2 1.3 17a17 17 0 0 0 5.2 2.6l1.1-1.8c-.6-.2-1.2-.5-1.7-.8l.4-.3a12 12 0 0 0 11.4 0l.4.3c-.5.3-1.1.6-1.7.8l1.1 1.8a17 17 0 0 0 5.2-2.6c.4-4.4-.7-8.3-3.1-11.7ZM8.5 14.7c-1 0-1.9-1-1.9-2.1s.8-2.1 1.9-2.1 1.9 1 1.9 2.1-.8 2.1-1.9 2.1Zm7 0c-1 0-1.9-1-1.9-2.1s.8-2.1 1.9-2.1 1.9 1 1.9 2.1-.8 2.1-1.9 2.1Z" />
  </svg>
);

export const TelegramIcon = ({ className = "" }: { className?: string }) => (
  <svg viewBox="0 0 24 24" className={className} fill="currentColor" aria-hidden="true">
    <path d="M12 1a11 11 0 1 0 0 22 11 11 0 0 0 0-22Zm5.1 7.5-1.8 8.6c-.1.6-.5.8-1 .5l-2.8-2.1-1.4 1.3c-.1.2-.3.3-.6.3l.2-2.9 5.2-4.7c.2-.2 0-.3-.3-.1l-6.5 4.1-2.8-.9c-.6-.2-.6-.6.1-.9l10.9-4.2c.5-.2 1 .1.8 1Z" />
  </svg>
);

// Замени на реальные ссылки
export const LINKS = {
  discord: "#", // Замени на ссылку-приглашение в Discord
  telegram: "#", // Замени на ссылку на Telegram-канал
  email: "team@govu1sen.ru", // Замени на реальную почту
};
            
