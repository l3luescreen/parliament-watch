<script land="ts">
	import dayjs from 'dayjs';
	import buddhistEra from 'dayjs/plugin/buddhistEra';
	import 'dayjs/locale/th';
	import Sidebar from '$components/LegislativeProcess/Sidebar.svelte';
	import VotingProcessImageCircle from '$components/LegislativeProcess/VotingProcessImageCircle.svelte';
	import ComparisonTable from '$components/ComparisonTable/ComparisonTable.svelte';
	import ProcessCard from '$components/LegislativeProcess/ProcessCard.svelte';
	import ProcessCardArrow from '$components/LegislativeProcess/ProcessCardArrow.svelte';

	dayjs.extend(buddhistEra);
	dayjs.locale('th');

  export let data;

	const proposerComparisonTableData = [
		{
			'': 'ครม.',
			'ร่าง พ.ร.บ.': 'มีสิทธิเสนอร่าง',
			'ออก พ.ร.ก.': 'มีสิทธิเสนอร่าง',
			'ร่าง พ.ร.ป.': 'มีสิทธิเสนอร่าง',
			'ร่างแก้ไขบทบัญญัติใน รธน.': 'มีสิทธิเสนอร่าง'
		},
		{
			'': 'สส.',
			'ร่าง พ.ร.บ.': '20 คน',
			'ออก พ.ร.ก.': '-',
			'ร่าง พ.ร.ป.': 'สส. ไม่น้อยกว่า 1 ใน 10',
			'ร่างแก้ไขบทบัญญัติใน รธน.': 'สส. ไม่น้อยกว่า 1 ใน 5'
		},
		{
			'': 'สมาชิกรัฐสภา',
			'ร่าง พ.ร.บ.': '-',
			'ออก พ.ร.ก.': '-',
			'ร่าง พ.ร.ป.': '-',
			'ร่างแก้ไขบทบัญญัติใน รธน.': 'สส. และ สว. ไม่น้อยกว่า 1 ใน 5'
		},
		{
			'': 'ประชาชนผู้มีสิทธิเลือกตั้ง',
			'ร่าง พ.ร.บ.': '10,000 คน',
			'ออก พ.ร.ก.': '-',
			'ร่าง พ.ร.ป.': '-',
			'ร่างแก้ไขบทบัญญัติใน รธน.': '50,000 คน'
		}
	];
</script>

<div class="flex flex-col w-full">
	<header class="bg-teal-20">
		<div class="w-full max-w-[800px] px-10 py-10 md:py-20 mx-auto">
			<h1 class="fluid-heading-05">ร่างกฎหมายกลายเป็นกฎหมายได้อย่างไร</h1>
			<p>
				<span class="text-text-primary font-bold">อัปเดตล่าสุด :</span>
				<span class="text-helper-text-01">{dayjs(new Date()).format('DD MMM BBBB')}</span>
			</p>
		</div>
	</header>
	<main class="flex flex-col justify-center md:flex-row items-center md:items-start">
		<div
			class="legislative-process-sidebar bg-ui-01 md:bg-white w-full md:w-auto gap-10 px-4 md:px-10 md:py-0 py-8"
		>
			<div class="py-10 w-full bg-white flex items-center justify-center">
				<Sidebar />
			</div>
		</div>
		<div
			class="w-full max-w-[800px] flex flex-col gap-10 px-4 md:px-10 py-8 bg-ui-01 md:bg-white flex-1"
		>
			<section>
				<h1 class="fluid-heading-05" id="แนะนำภาพรวม">แนะนำภาพรวม</h1>
				<div>
					<h2 class="fluid-heading-04" id="การออกกฎหมายตามรัฐธรรมนูญ 2560">
						การออกกฎหมายตามรัฐธรรมนูญ 2560
					</h2>
					<hr />
					<p class="body-02 mt-6">
						<b
							>‘รัฐสภา’ คือผู้รับผิดชอบหลักในการออกกฎหมาย
							เพราะเป็นตัวแทนของประชาชนในการทำหน้าที่และใช้อำนาจนิติบัญญัติ</b
						>
						การออกกฎหมายต้องดำเนินตามกระบวนการที่ระบุไว้ในรัฐธรรมนูญ 2560 ซึ่งกฎหมายมีหลายประเภท กฎหมายประเภทหนึ่งอาจมีกระบวนการ
						ลำดับขั้น หรือเงื่อนไขในการพิจารณาที่แตกต่างไปจากกฎหมายอีกประเภทหนึ่ง ด้วยเหตุเพราะกฎหมายแต่ละประเภทมีลำดับชั้นที่แตกต่างกัน
					</p>
					<br />
					<p class="body-02">
						<b>การกำหนดลำดับชั้นระหว่างกฎหมายประเภทต่าง ๆ</b> มีขึ้นเพื่อให้กฎหมายแม่บท อย่าง ‘รัฐธรรมนูญ’
						เป็นตัวกำกับกฎหมายที่อยู่ในลำดับชั้นรองลงมา เช่น พระราชบัญญัติ ซึ่งต้องห้ามขัดหรือแย้งต่อกฎหมายสูงสุดอย่างรัฐธรรมนูญ
						การพิจารณาบังคับใช้กฎหมายที่อยู่ในลำดับชั้นที่รองลงมาจึงมีกระบวนการบังคับใช้ที่ซับซ้อนน้อยกว่าการแก้ไขหรือการออกกฎหมายตัวแม่บทอย่างการแก้ไขบทบัญญัติในรัฐธรรมนูญ
					</p>
					<br />
					<p class="body-02">
						แม้กฎหมายจะมีหลายชื่อเรียก และมีลำดับชั้นที่หลากหลาย
						แต่กฎหมายแม่บททั้งหมดล้วนเกิดขึ้นจากกระบวนการการออกกฎหมายโดย ‘รัฐสภา’ เป็นสำคัญ
					</p>
				</div>
				<div>
					<h2 class="fluid-heading-04" id="กฎหมายบังคับใช้ได้อย่างไร">กฎหมายบังคับใช้ได้อย่างไร</h2>
					<hr />
					<h3 class="fluid-heading-03 my-6" id="การออกกฎหมายตามรัฐธรรมนูญ 2560">
						กฎหมายที่ออกโดยรัฐสภา ต้องผ่านกระบวนการ 3 ขั้นตอนสำคัญ
					</h3>
					<div class="grid grid-cols-1 md:grid-cols-[1fr_16px_1fr_16px_1fr] gap-3">
						<ProcessCard imgSrc="images/legislative-process/process-01.png" title="เสนอร่างกฎหมาย">
							ผู้มีสิทธิเสนอร่างของกฎหมายแต่ละประเภท จะแตกต่างกัน
						</ProcessCard>
						<ProcessCardArrow />
						<ProcessCard
							imgSrc="images/legislative-process/process-02.png"
							title="พิจารณาโดยรัฐสภา"
						>
							<ul class="list-disc list-inside">
								<li>สส.</li>
								<li>สว.</li>
								<li>สภาร่วม (สส.+ สว.)</li>
							</ul>
						</ProcessCard>
						<ProcessCardArrow />
						<ProcessCard
							imgSrc="images/legislative-process/process-03.png"
							title="กลายเป็นกฎหมายโดยสมบูรณ์"
						>
							<ul class="list-disc list-inside">
								<li>ไม่ขัดต่อรัฐธรรมนูญ</li>
								<li>พระมหากษัตริย์ทรงลงพระปรมาภิไธย</li>
							</ul>
						</ProcessCard>
					</div>
					<ol class="list-decimal list-inside body-02 mt-6">
						<li>
							<b>การเสนอร่างกฎหมาย</b> เป็นการจัดทำร่างกฎหมายและเสนอเข้าต่อรัฐสภา โดยผู้ที่มีสิทธิเสนอร่างกฎหมายจะแตกต่างกันขึ้นอยู่กับว่าเป็นร่างกฎหมายประเภทใดตามที่รัฐธรรมนูญระบุไว้
							เช่น ร่าง พ.ร.บ. สามารถเสนอโดยคณะรัฐมนตรี หรือ สส. จำนวนไม่น้อยกว่า 20 คน หรือ ประชาชนจำนวน10,000
							คน
						</li>
						<li>
							<b>การพิจารณาร่างกฎหมายโดยรัฐสภา</b> ร่างกฎหมายจะถูกพิจารณาโดยสมาชิกสภาผู้เแทนราษฎร (สส.)
							และสมาชิกวุฒิสภา (สว.) ตามลำดับ การพิจารณาของแต่ละสภาจะมี 3 วาระเท่ากัน แต่มีเงื่อนไขและรายละเอียดในการพิจารณาที่แตกต่างกัน
							ทั้งนี้ ในการพิจารณาร่างกฎหมายบางประเภท จะใช้การประชุมร่วมกันของทั้งสองสภาในการพิจารณา
							เช่น การพิจารณา ร่าง พ.ร.ป.
						</li>
						<li>
							<b>ร่างกฎหมายกลายเป็นกฎหมายโดยสมบูรณ์์</b> เมื่อร่างกฎหมายไม่ขัดต่อรัฐธรรมนูญ และพระมหากษัตริย์ทรงลงพระปรมาภิไธย
							ตามด้วยการประกาศในราชกิจจานุเบกษาให้มีผลบังคับใช้เป็นกฎหมาย
						</li>
					</ol>
				</div>
				<div>
					<h2 class="fluid-heading-04" id="กฎหมายในเว็บไซต์นี้">กฎหมายในเว็บไซต์นี้</h2>
					<hr />
					<p class="body-02 mt-6 mb-4">
						เว็บไซต์ Parliament Watch มุ่งนำเสนอกฎหมายที่ผ่านการพิจารณาโดยรัฐสภา
						เพื่อแสดงให้เห็นถึงกระบวนการทำงานด้านนิติบัญญัติในฐานะตัวแทนประชาชน
						รวมถึงสะท้อนให้เห็นถึงความคิดเห็นของสมาชิกรัฐสภาต่อประเด็นต่างๆ ในทางกฎหมาย
						ซึ่งเป็นเครื่องมือในการกำหนดทิศทางของสังคม ทั้งนี้
						เว็บไซต์นี้จะไม่ปรากฎกฎหมายที่ถูกตราขึ้นผ่านคณะรัฐมนตรีและไม่ต้องผ่านการพิจารณาโดยรัฐสภา
						เช่น พระราชกฤษฎีกา กฎกระทรวง และกฎหมายที่ตราโดยองค์กรปกครองส่วนท้องถิ่น
					</p>
					<img
						src="images/legislative-process/legislative-process-overview.png"
						alt="Overview of legislative process"
					/>
				</div>
				<div>
					<h2 class="fluid-heading-04" id="ประเภทของกฎหมายที่ผ่านการพิจารณาโดยรัฐสภา">
						ประเภทของกฎหมายที่ผ่านการพิจารณาโดยรัฐสภา
					</h2>
					<hr />
				</div>
				<div>
					<h2 class="fluid-heading-04" id="สถานะของกฎหมาย">สถานะของกฎหมาย</h2>
					<hr />
				</div>
			</section>
			<section>
				<h1 class="fluid-heading-05" id="ขั้นตอนการออกกฎหมายโดยรัฐสภา">
					ขั้นตอนการออกกฎหมายโดยรัฐสภา
				</h1>
				<div>
					<h2 class="fluid-heading-04" id="ขั้นตอนทั่วไป">ขั้นตอนทั่วไป</h2>
					<hr />
				</div>
				<div>
					ขั้นตอนการพิจารณาร่างกฎหมายแต่ละประเภทจะมีความแตกต่างกันในบางรายละเอียด แต่โดยทั่วไปแล้ว
					กระบวนการออกกฎหมายโดยรัฐสภา อย่างเช่นการออก พ.ร.บ. หรือการอนุมัติ พ.ร.ก. จะดำเนินการผ่าน <b
						>5 ขั้นตอน</b
					>ดังต่อไปนี้
				</div>
				<div class="flex w-full justify-center items-center py-4">
					<img
						src="images/legislative-process/general-process.png"
						alt="general-process-process"
						class="max-w-480"
					/>
				</div>
				<div class="py-6">
					<h3 class="fluid-heading-04 mb-0" id="การเสนอร่างกฎหมาย">1. การเสนอร่างกฎหมาย</h3>
					<p class="py-4">ผู้มีสิทธิเสนอร่างกฎหมาย และลำดับชั้นของกฎหมายที่เสนอได้</p>
					<div class="relative">
						<ComparisonTable {proposerComparisonTableData} />
					</div>
				</div>
				<div class="mb-6">
					<h2 class="fluid-heading-04" id="ขั้นตอนพิเศษของกฎหมายบางประเภท">
						ขั้นตอนพิเศษของกฎหมายบางประเภท
					</h2>
					<hr />
					<p class="my-6">
						ในกระบวนการออกกฎหมายหรือแก้กฎหมายบางประเภทจะใช้ <b
							>‘การประชุมร่วมกันของรัฐสภา’ หรือ สส. และ สว. ประชุมพิจารณาร่วมกัน</b
						>
						และ <b>มีเงื่อนไขเพิ่มเติม</b> ได้แก่
					</p>
					<div class="mt-10 body-02">
						<h3 class="fluid-heading-03 mb-6">การพิจารณาร่าง พ.ร.ป.</h3>
						<p>
							ขั้นตอนในการพิจารณาร่าง พ.ร.ป. จะดำเนินในรูปแบบเดียวกันกับการออก พ.ร.บ. เว้นแต่ใน<b
								>เงื่อนไขเพิ่มเติม</b
							>ต่อไปนี้
						</p>
						<img
							class="my-4 mx-auto w-full max-w-[440px]"
							src="images/legislative-process/organic-law-bill-consideration.png"
							alt="Organic law bill consideration"
						/>
						<ol class="list-decimal list-outside ml-6">
							<li class="mb-2">
								การพิจารณาโดยสภาร่วม (สส.+สว.) ต้องพิจารณา 3 วาระให้เสร็จภายใน 180 วัน
							</li>
							<li class="mb-2">
								ในวาระที่ 3
								ต้องมีคะแนนเสียงเห็นชอบด้วยมากกว่ากึ่งหนึ่งของจํานวนสมาชิกทั้งหมดเท่าที่มีอยู่ของรัฐสภา
							</li>
							<li class="mb-2">
								เมื่อรัฐสภา ‘เห็นชอบ’ ให้ส่งร่าง พ.ร.ป. ไปยังศาลฎีกา ศาลรัฐธรรมนูญ
								หรือองค์กรอิสระที่เกี่ยวข้องภายใน 15 วัน เพื่อให้ความเห็น
								<ul class="list-disc list-outside ml-8">
									<li>หากไม่มีข้อทักท้วงภายใน 10 วัน ให้รัฐสภาดําเนินการต่อไป</li>
									<li>
										มีข้อความขัดต่อรัฐธรรมนูญ ให้เสนอความเห็นไปยังรัฐสภา
										และให้รัฐสภาประชุมร่วมกันเพื่อพิจารณาให้แล้วเสร็จภายใน 30 วัน
										โดยสามารถแก้ไขตามที่เห็นสมควร
										จากนั้นให้รัฐสภาดําเนินการต่อไปในวิธีการเดียวกันกับการตรา พ.ร.บ.
									</li>
								</ul>
							</li>
						</ol>
					</div>
					<div class="mt-10 body-02">
						<h3 class="fluid-heading-03 mb-6">การแก้ไขบทบัญญัติในรัฐธรรมนูญ</h3>
						<p>
							เมื่อเข้าสู่ขั้นตอนการพิจารณาของรัฐสภา การประชุมร่วมกันจะมีทั้งหมด 3 วาระ
							เช่นเดียวกันกับการออก พ.ร.บ. แต่ปรากฏ<b>เงื่อนไขเพิ่มเติม</b>ดังนี้
						</p>
						<img
							class="my-4 mx-auto w-full max-w-[440px]"
							src="images/legislative-process/amendment-of-constitutional-provisions.png"
							alt="Amendment of constitutional provisions"
						/>
						<ol class="list-decimal list-outside gap-2 ml-6">
							<li class="mb-2">
								ในวาระที่หนึ่ง ต้องใช้เสียงไม่น้อยกว่าครึ่งหนึ่งของสมาชิกเท่าที่มีอยู่ของสองสภาแล้ว
								ในจำนวนนี้ต้องได้เสียง<b>เห็นชอบจาก สว. ไม่น้อยกว่า 1 ใน 3</b> ของจำนวน สว. ที่มีอยู่
							</li>
							<li class="mb-2">
								ในวาระที่สอง การลงมติให้ถือเสียงข้างมากเป็นประมาณ
								<b
									>หากเป็นการแก้ไขที่ประชาชนเป็นผู้เสนอ
									ต้องเปิดโอกาสให้ผู้แทนประชาชนเสนอความคิดเห็นด้วย</b
								> จากนั้นรอ 15 วัน จึงเข้าวาระที่สาม
							</li>
							<li class="mb-2">
								ในวาระที่สาม การลงมติ ‘เห็นชอบ’ ต้องประกอบด้วย
								<ul class="list-disc list-outside ml-8">
									<li>เสียงเห็นชอบมากกว่า<b>ครึ่งหนึ่งของสมาชิก</b>เท่าที่มีอยู่ของสองสภา</li>
									<li>เสียงเห็นชอบจาก ส.ว. ไม่น้อยกว่า <b>1 ใน 3 ของจำนวน ส.ว.</b></li>
									<li>
										เสียงเห็นชอบ ส.ส. จากพรรคที่ไม่มีสมาชิกเป็นรัฐมนตรี
										ประธานสภาหรือรองประธานผู้แทนฯ หรือ <b>“ส.ส. ฝ่ายค้าน” ไม่น้อยกว่าร้อยละ 20</b>
										ของทุกพรรคการเมืองดังกล่าวรวมกัน
									</li>
								</ul>
								เมื่อมีมติเห็นชอบให้รอไว้ 15 วันและนำขึ้นทูลเกล้าฯ ถวาย
							</li>
							<li class="mb-2">
								ในกรณีที่มีการแก้ไขเกี่ยวกับ บททั่วไป พระมหากษัตริย์ การแก้ไขเพิ่มเติมรัฐธรรมนูญ
								คุณสมบัติหรือลักษณะต้องห้ามของผู้ดำรงตำแหน่งต่างๆ
								หรืออำนาจหน้าที่ของศาลหรือองค์กรอิสระ ให้<b>จัดทำประชามติ</b>เพื่อเห็นชอบก่อน
								จึงจะสามารถประกาศใช้ได้
							</li>
							<li class="mb-2">
								ในระหว่างนี้ สส. หรือ สว. หรือทั้งสองสภารวมกัน <b>จำนวนไม่น้อยกว่า 1 ใน 10</b>
								สามารถใช้สิทธิเข้าชื่อเสนอให้<b>ศาลรัฐธรรมนูญวินิจฉัย</b>ว่าร่างแก้ไขรัฐธรรมนูญนั้น
								เป็นเรื่องเกี่ยวกับการเปลี่ยนแปลงการปกครองหรือไม่
								หรือเป็นเรื่องที่ต้องทำประชามติก่อนหรือไม่ โดยศาลรัฐธรรมนูญต้องพิจารณาให้เสร็จภายใน
								30 วันนับจากวันที่ได้รับเรื่อง โดยในระหว่างนี้ นายกฯ จะนำร่างฯ ขึ้นทูลเกล้าฯ ไม่ได้
							</li>
						</ol>
					</div>
				</div>
			</section>
			<section>
				<h1 class="fluid-heading-05" id="เข้าใจการลงมติของ สส. และ สว.">
					เข้าใจการลงมติของ สส. และ สว.
				</h1>
				<div class="mb-6">
					<h2 class="fluid-heading-04" id="การลงมติคืออะไร เกิดขึ้นในขั้นตอนไหนบ้าง ?">
						การลงมติคืออะไร เกิดขึ้นในขั้นตอนไหนบ้าง ?
					</h2>
					<hr />
					<div class="mt-6">
						<p>
							การลงมติ เป็นส่วนหนึ่งของการประชุมสภา ใช้ในกระบวนการพิจารณาเรื่องต่างๆ
							ทั้งในสภาผู้แทนราษฎร และวุฒิสภา เช่น การพิจารณาญัตติ, การเสนอและพิจารณาร่างกฎหมาย,
							การพิจารณาให้ความเห็นชอบนายกรัฐมนตรี, การพิจารณาในขั้นกรรมาธิการ เป็นต้น
							โดยมติของสภาจะกระทำโดยการออกเสียงลงคะแนน ตามวิธีการที่กำหนดไว้ในข้อบังคับการประชุม
							สมาชิกรัฐสภาหนึ่งคนมีสิทธิออกเสียงได้หนึ่งเสียง และมติของสภาให้เป็นไปตามเสียงข้างมาก
							เพื่อให้ได้ข้อยุติของปัญหาและเพื่อให้ได้แนวทางที่สภาจะต้องดำเนินการต่อไป
						</p>
					</div>
				</div>
				<div class="my-6 grid gap-4">
					<div>
						<h2 class="fluid-heading-04" id="วิธีการลงมติ">วิธีการลงมติ</h2>
						<hr />
						<div class="mt-6">
							<p>การลงมติในสภากระทำผ่านการออกเสียงลงคะแนน ซึ่งแบ่งเป็น 2 กรณี</p>
						</div>
					</div>
					<div class="grid gap-4">
						<p><strong>1. การออกเสียงลงคะแนนเปิดเผย</strong></p>
						<div class="flex gap-3 justify-center">
							<VotingProcessImageCircle
								src="https://placehold.co/120"
								title="การลงคะแนนเสียงด้วยวาจา"
								description="ผ่านการเรียกชื่อสมาชิกตามหมายเลขประจำตัว เช่น การโหวตเลือกนายกรัฐมนตรี"
							/>
							<VotingProcessImageCircle
								src="https://placehold.co/120"
								title="การใช้เครื่องลงคะแนนเสียง"
								description="เพื่อลงมติเห็นด้วยหรือไม่ต่อประเด็นต่างๆ"
							/>
						</div>
						<p><strong>2. การออกเสียงลงคะแนนลับ</strong></p>
						<div class="flex gap-3 justify-center">
							<VotingProcessImageCircle
								src="https://placehold.co/120"
								title="การทำเครื่องหมายบนแผ่นกระดาษ"
								description="ใส่ซองที่เจ้าหน้าที่จัดให้"
							/>
							<VotingProcessImageCircle
								src="https://placehold.co/120"
								title="การใช้เครื่องออกเสียงลงคะแนน"
								description="ตามที่ประชุมกำหนด"
							/>
						</div>
					</div>
					<div class="grid gap-2">
						<p><strong>เกณฑ์ในการเลือกวิธีการลงมติ</strong> ตามข้อบังคับการประชุมสภา</p>
						<div class="lg:flex gap-4">
							<div class="bg-ui-01 p-4 flex-1 mb-4 lg:mb-0 h-fit">
								<div class="mb-3">
									<p><strong>ที่ประชุมสภาผู้แทนฯ หรือที่ประชุมวุฒิสภา</strong></p>
								</div>
								<div>
									<ul class="list-disc pl-6">
										<li>การออกเสียงลงคะแนนให้กระทำเป็นการเปิดเผย</li>
										<li>
											ถ้ามีสมาชิกเสนอญัตติโดยมีผู้รับรองไม่น้อยกว่า 20 คนของสภานั้นๆ
											ขอให้กระทำเป็นการลับ จึงให้ลงคะแนนลับ
										</li>
										<li>
											แต่ถ้ามีผู้คัดค้านและมีผู้รับรองไม่น้อยกว่า 1 ใน 3 ของสมาชิกในที่ประชุม
											ให้ถือเป็นเอกสิทธิ์ที่จะลงคะแนนโดยเปิดเผย
										</li>
									</ul>
								</div>
							</div>
							<div class="bg-ui-01 p-4 flex-1 h-fit">
								<div class="mb-3">
									<p><strong>ประชุมสภาร่วม</strong></p>
								</div>
								<div>
									<ul class="list-disc pl-6">
										<li>การออกเสียงลงคะแนนให้กระทำเป็นการเปิดเผย</li>
										<li>
											ถ้าคณะรัฐมนตรีร้องขอ หรือสมาชิกรัฐสภาเสนอญัตติโดยมีสมาชิกรับรองไม่น้อยกว่า 40
											คนขอให้กระทำเป็นการลับ จึงให้ลงคะแนนลับ
										</li>
										<li>
											แต่ถ้ามีสมาชิกคัดค้านและมีผู้รับรองไม่น้อยกว่า 1 ใน 3
											ของสมาชิกรัฐสภาในที่ประชุมให้ถือเป็นเอกสิทธิ์ที่จะลงคะแนนโดยเปิดเผย
										</li>
									</ul>
								</div>
							</div>
						</div>
					</div>
				</div>

				<div>
					<h2 class="fluid-heading-04" id="ประเภทการลงมติ">ประเภทการลงมติ</h2>
					<hr />
				</div>
				<div>
					<h2 class="fluid-heading-04" id="ผลการลงมติ">ผลการลงมติ</h2>
					<hr />
				</div>
			</section>
			<section>
				<h1 class="fluid-heading-05" id="ส.ส. และ ส.ว. ทำอะไรบ้างในสภา">
					ส.ส. และ ส.ว. ทำอะไรบ้างในสภา
				</h1>
				<div>
					<h2 class="fluid-heading-04" id="หน้าที่ของสมาชิกสภาผู้แทนราษฏร (สส.)">
						หน้าที่ของสมาชิกสภาผู้แทนราษฏร (สส.)
					</h2>
					<hr />
					<div class="flex flex-col gap-2 py-4">
						{#each data.dutySection.representatives as section, i}
							<h3 class="fluid-heading-03" id={section.heading}>
								{i + 1}. {section.heading}
							</h3>
							<ul>
								{#each section.details as duty}
									<li>{duty}</li>
								{/each}
							</ul>
						{/each}
					</div>
				</div>
				<div>
					<h2 class="fluid-heading-04" id="หน้าที่ของสมาชิกวุฒิสภา (สว.)">
						หน้าที่ของสมาชิกวุฒิสภา (สว.)
					</h2>
					<hr />
					<div class="flex flex-col gap-2 py-4">
						{#each data.dutySection.senates as section, i}
							<h3 class="fluid-heading-03" id={section.heading}>
								{i + 1}. {section.heading}
							</h3>
							<ul>
								{#each section.details as duty}
									<li>{duty}</li>
								{/each}
							</ul>
						{/each}
					</div>
				</div>
				<div>
					<h2 class="fluid-heading-04" id="หน้าที่ของสภาร่วม (ส.ส. + ส.ว.)">
						หน้าที่ของสภาร่วม (ส.ส. + ส.ว.)
					</h2>
					<hr />
					<p class="pt-4">รัฐสภาจะประชุมร่วมกันได้ต้องเป็นไปตามที่กำหนดไว้ในมาตรา</p>
					<div class="flex flex-col gap-2 py-4">
						{#each data.dutySection.both as section, i}
							<h3 class="fluid-heading-03" id={section.heading}>
								{i + 1}. {section.heading}
							</h3>
							<ul>
								{#each section.details as duty}
									<li>{duty}</li>
								{/each}
							</ul>
						{/each}
					</div>
					<hr />
				</div>
			</section>
		</div>
		<div class="w-[250px]" />
	</main>
</div>

<style lang="postcss">
	section {
		@apply flex flex-col gap-4 bg-white px-4 md:px-0 py-8 md:py-0;
	}

	h1,
	h2,
	h3 {
		@apply text-text-primary mb-4;
	}

	hr {
		@apply border-0 border-solid border-gray-20 border-t w-full box-border;
	}

	ul {
		@apply list-disc list-outside ml-4;
	}
</style>
