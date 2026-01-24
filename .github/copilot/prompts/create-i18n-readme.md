---
name: create-i18n-readme
description: Create and synchronize multilingual documentation with cross-references
argument-hint: target languages (e.g., "Simplified Chinese, Traditional Chinese, Japanese, Korean")
---

You are tasked with creating multilingual versions of documentation files and maintaining cross-reference navigation between them.

**Note**: If no target languages are specified, create or update all standard language versions: Simplified Chinese, Traditional Chinese, Japanese, and Korean.

## Steps to follow:

1. **Analyze the source document** to understand its structure and content
2. **Create translated versions** for each specified target language:
   - Use appropriate terminology for the target locale
   - Maintain the same document structure and formatting
   - Preserve code blocks, URLs, and technical terms as-is
   - Apply locale-specific conventions (e.g., Traditional Chinese for Taiwan, Simplified Chinese for mainland China)

3. **Update language navigation links** at the top of each document:
   - Add links to all available language versions
   - Use native language names for each link (e.g., "English", "简体中文", "繁體中文", "日本語", "한국어")
   - Ensure all documents include complete, consistent navigation, excluding navigation to themselves.

4. **Follow naming conventions**:
   - Base document: `README.md`
   - Simplified Chinese: `*_CN.md`
   - Traditional Chinese: `*_TW.md`
   - Japanese: `*_JP.md`
   - Korean: `*_KR.md`
   - Other languages: Use appropriate ISO 639-1 codes

5. **Maintain consistency across all versions**:
   - Keep the same headings and section structure
   - Translate all user-facing content
   - Preserve technical accuracy

## Language-specific terminology guidelines:

### Simplified Chinese (Mainland China)

- 配置 (configuration)
- 软链 (symlink)
- 命令 (command)
- 文件 (file)
- 卸载 (uninstall)
- Use simplified characters only
- Follow mainland China usage conventions

### Traditional Chinese (Taiwan)

- 配置 → 設定
- 软链 → 符號連結
- 命令 → 指令
- 文件 → 檔案
- 卸载 → 解除安裝

### Japanese

- Use polite form (です・ます体)
- Technical terms in katakana when appropriate
- Use 「」for quotations

### Korean

- Use formal polite form (합니다체)
- Maintain spacing between Hangul and numbers/English
- Use native Korean words when available

After creating all language versions, verify that:

- All navigation links work correctly
- All versions have the same structure
- Technical content remains accurate across translations
