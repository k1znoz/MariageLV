<script lang="ts">
	// Navigation sections
	const sections = [
		{ id: 'accueil', label: 'Accueil' },
		{ id: 'dates-lieux', label: 'Dates & Lieux' },
		{ id: 'deroule', label: 'Déroulé' },
		{ id: 'acces', label: 'Accès' },
		{ id: 'hebergements', label: 'Hébergements' },
		{ id: 'dresscode', label: 'Dress Code' },
		{ id: 'enfants', label: 'Enfants' },
		{ id: 'questionnaire', label: 'Questionnaire' },
		{ id: 'contact', label: 'Contact' }
	];

	// Hébergements data
	const hebergementsProches = [
		{ nom: 'Gîte Les Acacias', capacite: '4/5 pers.', distance: 'Village', contact: '06 63 06 86 25' },
		{ nom: 'Chambre d\'hôtes rue d\'Enzia', capacite: '2/3 pers.', distance: 'Village', contact: '06 66 92 57 54' },
		{ nom: 'Moulin du Cray', capacite: '2 pers.', distance: '1 km', contact: '03 85 25 13 87' },
		{ nom: 'Maison d\'hôtes Terre des Barres', capacite: '-', distance: '2 km', contact: '06 99 37 48 06' },
		{ nom: 'Chambres d\'hôtes La Cathelinée', capacite: '-', distance: '2 km', contact: 'delphinemuth@gmail.com' },
		{ nom: 'Gîte Les Volets Rouges', capacite: '5 pers.', distance: '2,5 km', contact: '06 48 59 17 40' },
		{ nom: 'Chambres d\'hôtes Sylvie Bouteille', capacite: '4/6 pers.', distance: '3 km', contact: '06 11 60 68 00' },
		{ nom: 'Écuries La Villeneuve', capacite: 'Familial', distance: '3 km', contact: '06 22 48 91 43' }
	];

	const hebergementsEloignes = [
		{ nom: 'Le Baugy\'te (dortoir)', capacite: '14 pers.', distance: '5 km', contact: '06 41 99 54 82', petit_budget: true },
		{ nom: 'Chambres d\'hôtes Les Pergolas', capacite: '3 ch.', distance: '5 km', contact: 'homelespergolas@gmail.com' },
		{ nom: 'Villa Léonie (Marcigny)', capacite: '24 pers.', distance: '5 km', contact: '06 13 31 36 57' },
		{ nom: 'Gîte de la Terre des Pierres', capacite: '14 pers.', distance: '5,5 km', contact: '06 69 34 59 86' },
		{ nom: 'Gîte Le Chalet (Sainte-Foy)', capacite: '29 pers.', distance: '8,5 km', contact: '06 07 25 84 23' },
		{ nom: 'La Grange de Marraine & le Fenil de Joanny', capacite: '15-22 pers.', distance: '11 km', contact: '06 52 15 86 20' },
		{ nom: 'Château de Martigny', capacite: 'Chambres & gîte', distance: '12 min', contact: '03 85 81 53 21' },
		{ nom: 'Château de la Chaix', capacite: '-', distance: '18 min', contact: 'chateau-de-la-chaix.com' },
		{ nom: 'Château de Vaulx', capacite: '-', distance: '22 km', contact: 'chateaudevaulx.com' }
	];

	let mobileMenuOpen = $state(false);
</script>

<svelte:head>
	<title>Laetitia & Valentin — Mariage</title>
	<meta name="description" content="Nous avons le plaisir de vous convier à notre mariage les 10 et 11 octobre 2026." />
</svelte:head>

<!-- Navigation -->
<nav class="fixed top-0 left-0 right-0 z-50 bg-[var(--color-cream)]/95 backdrop-blur-sm border-b border-[var(--color-sage)]/20">
	<div class="max-w-6xl mx-auto px-4">
		<div class="flex items-center justify-between h-16">
			<a href="#accueil" class="font-serif text-xl text-[var(--color-charcoal)]">L & V</a>
			
			<!-- Desktop menu -->
			<div class="hidden md:flex items-center gap-6">
				{#each sections as section}
					<a 
						href="#{section.id}" 
						class="text-sm text-[var(--color-charcoal)]/70 hover:text-[var(--color-sage-dark)] transition-colors"
					>
						{section.label}
					</a>
				{/each}
			</div>

			<!-- Mobile menu button -->
			<button 
				class="md:hidden p-2" 
				onclick={() => mobileMenuOpen = !mobileMenuOpen}
				aria-label="Menu"
			>
				<svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
					{#if mobileMenuOpen}
						<path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M6 18L18 6M6 6l12 12" />
					{:else}
						<path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M4 6h16M4 12h16M4 18h16" />
					{/if}
				</svg>
			</button>
		</div>

		<!-- Mobile menu -->
		{#if mobileMenuOpen}
			<div class="md:hidden py-4 border-t border-[var(--color-sage)]/20">
				{#each sections as section}
					<a 
						href="#{section.id}" 
						class="block py-2 text-sm text-[var(--color-charcoal)]/70 hover:text-[var(--color-sage-dark)]"
						onclick={() => mobileMenuOpen = false}
					>
						{section.label}
					</a>
				{/each}
			</div>
		{/if}
	</div>
</nav>

<main>
	<!-- HERO / ACCUEIL -->
	<section id="accueil" class="min-h-screen flex items-center justify-center px-4 pt-16 bg-gradient-to-b from-[var(--color-cream)] to-[var(--color-sage)]/10">
		<div class="text-center max-w-2xl mx-auto">
			<p class="section-subtitle">Nous nous marions</p>
			<h1 class="font-serif text-5xl md:text-7xl font-medium text-[var(--color-charcoal)] mb-4">
				Laetitia <span class="text-[var(--color-gold)]">&</span> Valentin
			</h1>
			<div class="divider"></div>
			<p class="text-lg md:text-xl text-[var(--color-charcoal)]/80 mb-2">
				10 & 11 octobre 2026
			</p>
			<p class="text-base text-[var(--color-charcoal)]/60 mb-8">
				Gueugnon & Anzy-le-Duc, Bourgogne
			</p>
			<p class="text-base md:text-lg text-[var(--color-charcoal)]/70 leading-relaxed max-w-lg mx-auto mb-10">
				C'est avec une immense joie que nous vous invitons à partager ce moment unique avec nous. 
				Votre présence sera notre plus beau cadeau.
			</p>
			<a 
				href="#dates-lieux" 
				class="inline-flex items-center gap-2 text-[var(--color-sage-dark)] hover:text-[var(--color-charcoal)] transition-colors"
			>
				<span class="text-sm uppercase tracking-widest">Découvrir</span>
				<svg class="w-4 h-4 animate-bounce" fill="none" stroke="currentColor" viewBox="0 0 24 24">
					<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 14l-7 7m0 0l-7-7m7 7V3" />
				</svg>
			</a>
		</div>
	</section>

	<!-- DATES & LIEUX -->
	<section id="dates-lieux" class="py-20 px-4">
		<div class="max-w-4xl mx-auto">
			<p class="section-subtitle">Où & Quand</p>
			<h2 class="section-title">Dates & Lieux</h2>
			<div class="divider"></div>

			<div class="grid md:grid-cols-2 gap-8 mt-12">
				<!-- Cérémonie -->
				<div class="bg-white rounded-2xl p-8 shadow-sm border border-[var(--color-sage)]/10">
					<div class="w-12 h-12 bg-[var(--color-sage)]/20 rounded-full flex items-center justify-center mb-4">
						<span class="text-2xl">⛪</span>
					</div>
					<h3 class="font-serif text-2xl text-[var(--color-charcoal)] mb-2">Cérémonie religieuse</h3>
					<p class="text-[var(--color-sage-dark)] font-medium mb-4">Samedi 10 octobre 2026</p>
					<div class="space-y-1 text-[var(--color-charcoal)]/70">
						<p class="font-medium text-[var(--color-charcoal)]">Église Saint-Maurice</p>
						<p>Place de l'église</p>
						<p>71130 Gueugnon</p>
					</div>
					<p class="mt-4 text-sm text-[var(--color-charcoal)]/60 flex items-center gap-2">
						<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
							<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z" />
						</svg>
						Parking à proximité
					</p>
				</div>

				<!-- Réception -->
				<div class="bg-white rounded-2xl p-8 shadow-sm border border-[var(--color-sage)]/10">
					<div class="w-12 h-12 bg-[var(--color-terracotta)]/20 rounded-full flex items-center justify-center mb-4">
						<span class="text-2xl">🥂</span>
					</div>
					<h3 class="font-serif text-2xl text-[var(--color-charcoal)] mb-2">Vin d'honneur & Réception</h3>
					<p class="text-[var(--color-sage-dark)] font-medium mb-4">Samedi 10 & Dimanche 11 octobre</p>
					<div class="space-y-1 text-[var(--color-charcoal)]/70">
						<p class="font-medium text-[var(--color-charcoal)]">Les Salles du Prieuré</p>
						<p>Le Bourg – Le Prieuré</p>
						<p>71110 Anzy-le-Duc</p>
					</div>
					<p class="mt-4 text-sm text-[var(--color-charcoal)]/60 flex items-center gap-2">
						<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
							<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z" />
						</svg>
						Parking sur place
					</p>
				</div>
			</div>
		</div>
	</section>

	<!-- DÉROULÉ DU WEEK-END -->
	<section id="deroule" class="py-20 px-4 bg-[var(--color-sage)]/10">
		<div class="max-w-3xl mx-auto">
			<p class="section-subtitle">Le programme</p>
			<h2 class="section-title">Déroulé du week-end</h2>
			<div class="divider"></div>

			<div class="mt-12 space-y-8">
				<!-- Samedi -->
				<div class="bg-white rounded-2xl p-8 shadow-sm">
					<h3 class="font-serif text-2xl text-[var(--color-charcoal)] mb-6 flex items-center gap-3">
						<span class="w-10 h-10 bg-[var(--color-sage)]/20 rounded-full flex items-center justify-center text-sm font-sans">Sam</span>
						Samedi 10 octobre
					</h3>
					<div class="space-y-4">
						<div class="flex gap-4">
							<div class="w-16 text-[var(--color-sage-dark)] font-medium text-sm">14h30</div>
							<div>
								<p class="font-medium text-[var(--color-charcoal)]">Cérémonie religieuse</p>
								<p class="text-sm text-[var(--color-charcoal)]/60">Église Saint-Maurice, Gueugnon</p>
							</div>
						</div>
						<div class="flex gap-4">
							<div class="w-16 text-[var(--color-sage-dark)] font-medium text-sm">16h00</div>
							<div>
								<p class="font-medium text-[var(--color-charcoal)]">Trajet vers la réception</p>
								<p class="text-sm text-[var(--color-charcoal)]/60">Environ 40 minutes</p>
							</div>
						</div>
						<div class="flex gap-4">
							<div class="w-16 text-[var(--color-sage-dark)] font-medium text-sm">17h00</div>
							<div>
								<p class="font-medium text-[var(--color-charcoal)]">Vin d'honneur</p>
								<p class="text-sm text-[var(--color-charcoal)]/60">Les Salles du Prieuré, Anzy-le-Duc</p>
							</div>
						</div>
						<div class="flex gap-4">
							<div class="w-16 text-[var(--color-sage-dark)] font-medium text-sm">20h00</div>
							<div>
								<p class="font-medium text-[var(--color-charcoal)]">Dîner & Soirée dansante</p>
								<p class="text-sm text-[var(--color-charcoal)]/60">Jusqu'au bout de la nuit ✨</p>
							</div>
						</div>
					</div>
				</div>

				<!-- Dimanche -->
				<div class="bg-white rounded-2xl p-8 shadow-sm">
					<h3 class="font-serif text-2xl text-[var(--color-charcoal)] mb-6 flex items-center gap-3">
						<span class="w-10 h-10 bg-[var(--color-terracotta)]/20 rounded-full flex items-center justify-center text-sm font-sans">Dim</span>
						Dimanche 11 octobre
					</h3>
					<div class="space-y-4">
						<div class="flex gap-4">
							<div class="w-16 text-[var(--color-sage-dark)] font-medium text-sm">11h00</div>
							<div>
								<p class="font-medium text-[var(--color-charcoal)]">Brunch convivial</p>
								<p class="text-sm text-[var(--color-charcoal)]/60">Pour prolonger le bonheur ensemble</p>
							</div>
						</div>
					</div>
				</div>
			</div>
		</div>
	</section>

	<!-- ACCÈS & TRAJETS -->
	<section id="acces" class="py-20 px-4">
		<div class="max-w-3xl mx-auto">
			<p class="section-subtitle">Comment venir</p>
			<h2 class="section-title">Accès & Trajets</h2>
			<div class="divider"></div>

			<div class="mt-12 space-y-6">
				<div class="bg-white rounded-2xl p-8 shadow-sm border border-[var(--color-sage)]/10">
					<h3 class="font-serif text-xl text-[var(--color-charcoal)] mb-4 flex items-center gap-3">
						<span class="text-2xl">🚗</span>
						Trajet entre les lieux
					</h3>
					<p class="text-[var(--color-charcoal)]/70 mb-4">
						Le trajet entre l'église de Gueugnon et la salle de réception d'Anzy-le-Duc prend 
						<strong class="text-[var(--color-charcoal)]">environ 40 minutes</strong>.
					</p>
					<p class="text-sm text-[var(--color-charcoal)]/60">
						Nous vous invitons à prévoir ce temps de route et à covoiturer si possible.
					</p>
				</div>

				<!-- Alerte Péage -->
				<div class="bg-[var(--color-terracotta)]/10 rounded-2xl p-8 border border-[var(--color-terracotta)]/30">
					<h3 class="font-serif text-xl text-[var(--color-charcoal)] mb-4 flex items-center gap-3">
						<span class="text-2xl">⚠️</span>
						Péage en flux libre
					</h3>
					<p class="text-[var(--color-charcoal)]/80 mb-4">
						L'autoroute est équipée d'un <strong>péage en flux libre ALIAE</strong> (sans barrière).
					</p>
					<div class="bg-white rounded-xl p-4">
						<p class="text-sm text-[var(--color-charcoal)]/70">
							<strong class="text-[var(--color-charcoal)]">Important :</strong> Le paiement doit être effectué 
							<strong>sous 48h</strong> en ligne sur le site ALIAE, ou automatiquement si vous disposez d'un télépéage.
						</p>
					</div>
				</div>
			</div>
		</div>
	</section>

	<!-- HÉBERGEMENTS -->
	<section id="hebergements" class="py-20 px-4 bg-[var(--color-sage)]/10">
		<div class="max-w-5xl mx-auto">
			<p class="section-subtitle">Où dormir</p>
			<h2 class="section-title">Hébergements</h2>
			<div class="divider"></div>
			<p class="text-center text-[var(--color-charcoal)]/70 max-w-xl mx-auto mb-12">
				Voici une sélection d'hébergements à proximité du lieu de réception. 
				N'hésitez pas à réserver rapidement !
			</p>

			<!-- Proches -->
			<div class="mb-12">
				<h3 class="font-serif text-xl text-[var(--color-charcoal)] mb-6 flex items-center gap-2">
					<span class="w-2 h-2 bg-[var(--color-sage)] rounded-full"></span>
					À proximité immédiate
				</h3>
				<div class="grid sm:grid-cols-2 lg:grid-cols-4 gap-4">
					{#each hebergementsProches as h}
						<div class="bg-white rounded-xl p-5 shadow-sm border border-[var(--color-sage)]/10 hover:shadow-md transition-shadow">
							<h4 class="font-medium text-[var(--color-charcoal)] text-sm mb-2 leading-tight">{h.nom}</h4>
							<div class="space-y-1 text-xs text-[var(--color-charcoal)]/60">
								{#if h.capacite !== '-'}
									<p>👥 {h.capacite}</p>
								{/if}
								<p>📍 {h.distance}</p>
								<p class="text-[var(--color-sage-dark)]">📞 {h.contact}</p>
							</div>
						</div>
					{/each}
				</div>
			</div>

			<!-- Plus éloignés -->
			<div>
				<h3 class="font-serif text-xl text-[var(--color-charcoal)] mb-6 flex items-center gap-2">
					<span class="w-2 h-2 bg-[var(--color-terracotta)] rounded-full"></span>
					À quelques kilomètres
				</h3>
				<div class="grid sm:grid-cols-2 lg:grid-cols-3 gap-4">
					{#each hebergementsEloignes as h}
						<div class="bg-white rounded-xl p-5 shadow-sm border border-[var(--color-sage)]/10 hover:shadow-md transition-shadow">
							{#if h.petit_budget}
								<span class="inline-block text-xs bg-[var(--color-sage)]/20 text-[var(--color-sage-dark)] px-2 py-0.5 rounded mb-2">Petit budget</span>
							{/if}
							<h4 class="font-medium text-[var(--color-charcoal)] text-sm mb-2 leading-tight">{h.nom}</h4>
							<div class="space-y-1 text-xs text-[var(--color-charcoal)]/60">
								{#if h.capacite !== '-'}
									<p>👥 {h.capacite}</p>
								{/if}
								<p>📍 {h.distance}</p>
								<p class="text-[var(--color-sage-dark)]">📞 {h.contact}</p>
							</div>
						</div>
					{/each}
				</div>
			</div>
		</div>
	</section>

	<!-- DRESS CODE -->
	<section id="dresscode" class="py-20 px-4">
		<div class="max-w-2xl mx-auto text-center">
			<p class="section-subtitle">Tenue</p>
			<h2 class="section-title">Dress Code</h2>
			<div class="divider"></div>

			<div class="mt-10 bg-white rounded-2xl p-10 shadow-sm border border-[var(--color-sage)]/10">
				<div class="w-16 h-16 bg-[var(--color-gold)]/10 rounded-full flex items-center justify-center mx-auto mb-6">
					<span class="text-3xl">👗</span>
				</div>
				<p class="text-[var(--color-charcoal)]/80 text-lg leading-relaxed">
					Un <strong class="text-[var(--color-charcoal)]">mood board</strong> vous sera communiqué 
					avec le faire-part afin de vous guider dans le choix de votre tenue.
				</p>
				<p class="mt-4 text-sm text-[var(--color-charcoal)]/60">
					Restez à l'écoute ! ✨
				</p>
			</div>
		</div>
	</section>

	<!-- ENFANTS & GARDE -->
	<section id="enfants" class="py-20 px-4 bg-[var(--color-sage)]/10">
		<div class="max-w-2xl mx-auto text-center">
			<p class="section-subtitle">Les petits</p>
			<h2 class="section-title">Enfants & Garde</h2>
			<div class="divider"></div>

			<div class="mt-10 bg-white rounded-2xl p-10 shadow-sm">
				<div class="w-16 h-16 bg-[var(--color-sage)]/20 rounded-full flex items-center justify-center mx-auto mb-6">
					<span class="text-3xl">👶</span>
				</div>
				<p class="text-[var(--color-charcoal)]/80 text-lg mb-8">
					Les enfants sont les bienvenus pour tout le week-end !
				</p>

				<div class="grid sm:grid-cols-2 gap-4 text-left">
					<div class="bg-[var(--color-cream)] rounded-xl p-5">
						<p class="font-medium text-[var(--color-charcoal)] mb-1">👩‍👧 Nounous disponibles</p>
						<p class="text-sm text-[var(--color-charcoal)]/60">
							Des nounous seront présentes pour s'occuper des enfants.
						</p>
					</div>
					<div class="bg-[var(--color-cream)] rounded-xl p-5">
						<p class="font-medium text-[var(--color-charcoal)] mb-1">🏠 Salle dédiée</p>
						<p class="text-sm text-[var(--color-charcoal)]/60">
							Un espace de garde est prévu à côté de la salle de dîner.
						</p>
					</div>
				</div>

				<div class="mt-8 p-4 bg-[var(--color-terracotta)]/10 rounded-xl border border-[var(--color-terracotta)]/20">
					<p class="text-sm text-[var(--color-charcoal)]/70">
						<strong class="text-[var(--color-charcoal)]">À noter :</strong> 
						Les frais de garde seront à la charge des parents.
					</p>
				</div>

				<p class="mt-6 text-sm text-[var(--color-charcoal)]/60 italic">
					Merci de votre compréhension 💛
				</p>
			</div>
		</div>
	</section>

	<!-- QUESTIONNAIRE -->
	<section id="questionnaire" class="py-20 px-4">
		<div class="max-w-2xl mx-auto text-center">
			<p class="section-subtitle">Confirmez votre présence</p>
			<h2 class="section-title">Questionnaire</h2>
			<div class="divider"></div>

			<div class="mt-10 bg-gradient-to-br from-[var(--color-sage)]/20 to-[var(--color-terracotta)]/10 rounded-2xl p-10">
				<p class="text-[var(--color-charcoal)]/80 text-lg mb-8">
					Pour nous aider à organiser au mieux cette journée, merci de remplir le questionnaire ci-dessous.
				</p>
				<a 
					href="https://docs.google.com/forms/d/e/1FAIpQLSewyccDsNKdWDfoCYeaBDZAnuDI57GG-U_aRBujMzAdl7Kf0A/viewform"
					target="_blank"
					rel="noopener noreferrer"
					class="inline-flex items-center gap-2 bg-[var(--color-sage-dark)] hover:bg-[var(--color-charcoal)] text-white px-8 py-4 rounded-full font-medium transition-colors shadow-lg hover:shadow-xl"
				>
					Répondre au questionnaire
					<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
						<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3" />
					</svg>
				</a>
				<p class="mt-6 text-sm text-[var(--color-charcoal)]/60">
					Le questionnaire prend moins de 2 minutes à compléter.
				</p>
			</div>
		</div>
	</section>

	<!-- CONTACT -->
</main>

<!-- Footer -->
<footer class="bg-[var(--color-charcoal)] text-white/40 py-6 px-4 text-center text-sm border-t border-white/10">
	<p>Laetitia & Valentin — 10 & 11 octobre 2026</p>
	<p class="mt-1">Fait avec 💛</p>
</footer>
